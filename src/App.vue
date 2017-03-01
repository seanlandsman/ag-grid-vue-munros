<template>
    <div id="app">
        <div id="contentwrapper">
            <div id="contentcolumn">
                <div class="innertube">
                    <munro-detail :selectedMunro="selectedMunro"></munro-detail>
                </div>
            </div>
        </div>
        <div id="leftcolumn">
            <div class="innertube">
                <munro-grid @munroSelected="munroSelected"></munro-grid>
            </div>
        </div>
    </div>
</template>

<script>
    import MunroGrid from './components/MunroGrid';
    import MunroDetail from './components/MunroDetail';

    export default {
        name: 'app',
        data() {
            return {
                selectedMunro: null
            }
        },
        components: {
            MunroGrid,
            MunroDetail
        },
        methods: {
            munroSelected(munro) {
                this.selectedMunro = munro;
            }
        }
    }
</script>

<style scoped>
    body {
        margin: 0;
        padding: 0;
        line-height: 1.5em;
    }

    #contentwrapper {
        float: left;
        width: 100%;
    }

    #contentcolumn {
        margin-left: 60%;
        max-width: 40%;
    }

    #leftcolumn {
        float: left;
        width: 60%;
        margin-left: -100%;
    }

    .innertube {
        margin: 10px;
        margin-top: 0;
    }

    @media (max-width: 600px) {
        #contentwrapper {
            float: none;
        }

        #leftcolumn {
            float: none;
            width: 100%;
            margin-left: 0;
        }

        #contentcolumn {
            margin-left: 0;
        }
    }
</style>