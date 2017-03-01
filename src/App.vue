<template>
    <div id="app">
        <section class="hero is-fullheight is-bold is-dark">
            <div class="hero-body">
                <div class="container has-text-centered">
                    <div class="columns">
                        <div class="column is-3 is-offset-3">
                            <div class="green-button notification is-success">

                            </div>
                        </div>
                        <div class="column is-3">
                            <div class="red-button notification is-danger">

                            </div>
                        </div>
                    </div>
                    <div class="columns">
                        <div class="column is-3 is-offset-3">
                            <div class="yellow-button notification is-warning">

                            </div>
                        </div>
                        <div class="column is-3">
                            <div class="blue-button notification is-info">

                            </div>
                        </div>
                    </div>
                    <a class="button is-dark is-inverted is-outlined has-text-centered is-large">Start</a>
                    <a class="button is-dark is-inverted is-outlined has-text-centered is-large">Help</a>
                    <a class="button is-dark is-inverted is-outlined has-text-centered is-large">Score: {{score}}</a>
                </div>
            </div>
        </section>
    </div>
</template>

<script>
    export default {
        name: 'app',
        data () {
            return {
                score: 0
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

    .green-button, .red-button, .yellow-button, .blue-button {
        height: 30vh;
    }

</style>
