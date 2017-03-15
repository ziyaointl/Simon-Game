<template>
    <div id="app">
        <section class="hero is-fullheight is-bold is-dark">
            <div class="hero-body">
                <div class="container has-text-centered">
                    <div class="columns">
                        <div class="column is-3 is-offset-3">
                            <div class="notification is-success active-green" id="green-button" @click="padClicked(0)">

                            </div>
                        </div>
                        <div class="column is-3">
                            <div class="notification is-danger active-red" id="red-button" @click="padClicked(1)">

                            </div>
                        </div>
                    </div>
                    <div class="columns">
                        <div class="column is-3 is-offset-3">
                            <div class="notification is-warning active-yellow" id="yellow-button" @click="padClicked(2)">

                            </div>
                        </div>
                        <div class="column is-3">
                            <div class="notification is-info active-blue" id="blue-button" @click="padClicked(3)">

                            </div>
                        </div>
                    </div>
                    <a class="button is-dark is-inverted is-outlined has-text-centered is-large" @click="startGame">Start</a>
                    <a class="button is-dark is-inverted is-outlined has-text-centered is-large" @click="showHelp">Help</a>
                    <a class="button is-dark is-inverted is-outlined has-text-centered is-large">Score: {{score}}</a>

                    <div class="modal" id="help">
                        <div class="modal-background"></div>
                        <div class="modal-content">
                            <article class="message">
                                <div class="message-body">
                                    Lorem ipsum dolor sit amet, consectetur adipiscing elit. <strong>Pellentesque risus
                                    mi</strong>, tempus quis placerat ut, porta nec nulla. Vestibulum rhoncus ac ex sit
                                    amet fringilla. Nullam gravida purus diam, et dictum <a>felis venenatis</a>
                                    efficitur. Aenean ac <em>eleifend lacus</em>, in mollis lectus. Donec sodales, arcu
                                    et sollicitudin porttitor, tortor urna tempor ligula, id porttitor mi magna a neque.
                                    Donec dui urna, vehicula et sem eget, facilisis sodales sem.
                                </div>
                            </article>
                        </div>
                        <button class="modal-close" @click="closeHelp"></button>
                    </div>
                </div>
            </div>
        </section>
    </div>
</template>

<script>
    export default {
        name: 'app',
        data() {
            return {
                score: 0,
                pads: [
                    {
                        id:"green-button",
                        color: "rgb(35, 209, 96)",
                        lighten: "#47e07d"
                    },
                    {
                        id: "red-button",
                        color: "rgb(255, 56, 96)",
                        lighten: "#ff6b89"
                    },
                    {
                        id:"yellow-button",
                        color: "rgb(255, 221, 87)",
                        lighten: "#ffe78a"
                    },
                    {
                        id:"blue-button",
                        color: "rgb(50, 115, 220)",
                        lighten: "#5e91e3"
                    }
                ],
                numbers: [],
                padsDisabled: true,
                inputDisabled: false,
                currentNumberIndex: 0
            }
        },
        methods: {
            startGame() {
                if (!this.inputDisabled) {
                    this.reset();
                    this.runLoop();
                }
            },
            shadeRGBColor(color, percent) {
                let f = color.split(","), t = percent < 0 ? 0 : 255, p = percent < 0 ? percent * -1 : percent, R = parseInt(f[0].slice(4)), G = parseInt(f[1]), B = parseInt(f[2]);
                return "rgb(" + (Math.round((t - R) * p) + R) + "," + (Math.round((t - G) * p) + G) + "," + (Math.round((t - B) * p) + B) + ")";
            },
            getRandomInt(min, max) {
                min = Math.ceil(min);
                max = Math.floor(max);
                return Math.floor(Math.random() * (max - min)) + min;
            },
            timeoutLoop(fn, n, delay) {
                let vm = this;
                if (n > 0) {
                    setTimeout(function () {
                        fn();
                        vm.timeoutLoop(fn, n - 1, delay);
                    }, delay);
                }
            },
            padClicked(index) {
                if (!this.padsDisabled) {
                    if (this.currentNumberIndex < this.numbers.length) {
                        if (index === this.numbers[this.currentNumberIndex]) {
                            this.currentNumberIndex++;
                        }
                        else {
                            //TODO: End game
                            alert("end");
                            this.reset();
                            return;
                        }
                    }
                    if (this.currentNumberIndex === this.numbers.length) {
                        ++this.score;
                        this.currentNumberIndex = 0;
                        this.runLoop();
                    }
                }
            },
            showHelp() {
                //TODO: Implement show help
                document.getElementById("help").classList.add("is-active")
            },
            resetPadColor(index) {
                let element = document.getElementById(this.pads[index].id);
                element.style.backgroundColor = "";
            },
            lightenPadColor(index) {
                let element = document.getElementById(this.pads[index].id);
                element.style.backgroundColor = this.pads[index].lighten;
            },
            runLoop() {
                let vm = this;
                vm.numbers.push(vm.getRandomInt(0, 4));
                vm.inputDisabled = false;
                vm.padsDisabled = true;

                vm.timeoutLoop(function () {
                    if (vm.currentNumberIndex < vm.numbers.length) {
                        let index = vm.numbers[vm.currentNumberIndex];
                        vm.lightenPadColor(index);
                        setTimeout(function () {
                            vm.resetPadColor(index);
                        }, 1000);
                        vm.currentNumberIndex++;
                        console.log(vm.currentNumberIndex);
                    }
                    else {
                        vm.currentNumberIndex = 0;
                        vm.inputDisabled = false;
                        vm.padsDisabled = false;
                    }
                }, vm.numbers.length + 1, 1500);
            },
            reset() {
                this.score = 0;
                this.numbers = [];
                this.currentNumberIndex = 0;
                this.padsDisabled = true;
            },
            closeHelp() {
                document.getElementById("help").classList.remove("is-active");
            }
        }
    }
</script>

<style lang="scss">
    @import "css/bulma/utilities/_all.sass";
    @import "css/bulma/base/_all.sass";
    @import "css/bulma/layout/_all.sass";
    @import "css/bulma/elements/_all.sass";
    @import "css/bulma/grid/_all.sass";
    @import "css/bulma/components/_all.sass";

    $green-color: rgb(35, 209, 96);
    $red-color: rgb(255, 56, 96);
    $blue-color: rgb(50, 115, 220);
    $yellow-color: rgb(255, 221, 87);

    #green-button, #red-button, #yellow-button, #blue-button {
        height: 30vh;
    }

    #green-button:active, .active-green-button {
        background-color: lighten($green-color, 10%);
    }
    #blue-button:active, .active-blue-button {
        background-color: lighten($blue-color, 10%);
    }
    #red-button:active, .active-red-button {
        background-color: lighten($red-color, 10%);
    }
    #yellow-button:active, .active-yellow-button {
        background-color: lighten($yellow-color, 10%);
    }


</style>
