<template>
    <div id="app">
        <div class="container">
            <div class="columns">
                <div class="column is-6">
                    <div class="green-button notification is-success">

                    </div>
                </div>
                <div class="column is-6">
                    <div class="red-button notification is-danger">

                    </div>
                </div>
            </div>
            <div class="columns">
                <div class="column is-6">
                    <div class="yellow-button notification is-warning">

                    </div>
                </div>
                <div class="column is-6">
                    <div class="blue-button notification is-info">

                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'app',
        data () {
            return {

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

    .green-button, .red-button {
    
    }
</style>
