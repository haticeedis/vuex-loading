<template>
    <div>
        <div class="container">
            <v-loading message='Something loading! Lovely...'>
                <template slot='spinner'>
                    <loading-heart width='1em' height='1em'/>
                </template>
                This will be shown after load.
            </v-loading>
        </div>
        <button @click='$vueLoading.startLoading("writing code")' :disable='$vueLoading.isLoading("writing code")'>
            <v-loading loader='writing code' message='Writing Code...'>
                <template slot='spinner'>
                    <loading-spinner width="1em" height="1em"/>
                </template>
                Write Code
            </v-loading>
        </button>
        <button @click='endLoading' :disabled='!$vueLoading.isLoading("writing code")'>
            <span v-if='$vueLoading.isLoading("writing code")'>Stop Coding</span>
            <span v-else>Coding Stopped</span>
        </button>
        <br>
        <button @click='$vueLoading.startLoading("c")' :disabled='$vueLoading.isLoading("c")'>
            Start <b>"c"</b> Loader
        </button>
        <button @click='$vueLoading.endLoading("c")' :disabled='!$vueLoading.isLoading("c")'>
            Stop <b>"c"</b> Loader
        </button>
        <p>
            Toggle on any letter to load/unload together.
        </p>
        <ul class="list">
            <li v-for='loader in loaders' @click='toggleLoader(loader)'>
                <v-loading :loader='loader' message=''>
                    <template slot='spinner' v-if='loader == "c"'>
                        <loading-heart width="1em" height="1em"/>
                    </template>
                    <template slot='spinner' v-else>
                        <loading-spinner width="1em" height="1em"/>
                    </template>
                    {{ loader }}
                </v-loading>
            </li>
        </ul>
    </div>

</template>
<script>
    import vLoading from '../../src/v-loading.vue'
    import loadingHeart from '../../src/spinners/heart.vue'
    import loadingSpinner from '../../src/spinners/spinner.vue'

    export default {
        name: 'main',
        components: {
            'v-loading': vLoading,
            'loading-heart': loadingHeart,
            'loading-spinner': loadingSpinner
        },
        data() {
            return {
                loaders: ['a', 'c', 'b', 'a', 'b', 'a', 'c', 'a', 'c', 'a', 'b']
            };
        },
        methods: {
            writeCode() {
                this.$vueLoading.startLoading('writing code');
            },
            endLoading() {
                this.$vueLoading.endLoading('writing code');
            },
            toggleLoader(loader) {
                if (this.$vueLoading.isLoading(loader)) {
                    this.$vueLoading.endLoading(loader);
                } else {
                    this.$vueLoading.startLoading(loader);
                }
            }
        }

    }
</script>


<style>
    body {
        font-family: Arial, Helvetica, sans-serif;
        font-size: 20px;
    }

    #app {
        margin: 50px auto;
        width: 500px;
        text-align: center;
    }

    .list {
        list-style: none;
        padding: 0;
    }

    .list li {
        display: inline-block;
        margin: 10px;
        width: 30px;
        height: 30px;
        border-radius: 3px;
        border: 2px solid #ccc;
        line-height: 30px;
    }

    .container {
        padding: 50px;
    }

    button {
        border: 0;
        background-color: #fff;
        border: 2px solid #9f0fa0;
        border-radius: 4px;
        margin: 5px;
        color: #9f0fa0;
        font-size: 16px;
        padding: 8px;
    }

    button[disabled] {
        opacity: 0.4;
    }

    .my-loading {
        text-align: center;
        opacity: .5;
        animation: pulse 3s infinite;
        animation-delay: 1s;
    }

    @-webkit-keyframes pulse {
        0%, 100% {
            opacity: .5;
        }
        50% {
            opacity: .1;
        }
    }

    @keyframes pulse {
        0%, 100% {
            opacity: .5;
        }
        50% {
            opacity: .1;
        }
    }
</style>
