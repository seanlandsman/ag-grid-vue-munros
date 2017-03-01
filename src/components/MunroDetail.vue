<template>
    <div class="detail" v-if="selectedMunro">
        <table class="table">
            <tr>
                <td colspan="2">
                    {{selectedMunro.hillname}}
                </td>
            </tr>
            <tr>
                <td class="key">
                    Elevation
                </td>
                <td>
                    {{selectedMunro.height}}
                </td>
            </tr>
            <tr>
                <td class="key">
                    <div class="title">Latitude</div>
                </td>
                <td>
                    {{selectedMunro.latitude}}
                </td>
            </tr>
            <tr>
                <td class="key">
                    Longitude
                </td>
                <td>
                    {{selectedMunro.longitude}}
                </td>
            </tr>
            <tr>
                <td colspan="2">
                    <span v-if="!showImage" class="image-prompt" @click="showImage=true">Click Here For Image of {{selectedMunro.hillname}}</span>
                </td>
            </tr>
        </table>
        <div class="image-area">
            <img v-if="showImage" class="image" :src="selectedMunro.image"/>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'munro-detail',
        props: ['selectedMunro'],
        data () {
            return {
                showImage: false
            }
        },
        updated() {
            this.showImage=false;
        }
    }
</script>

<style scoped>
    .detail {
        display: inline-block;
        width: 100%;
    }

    .table {
        border: 1px solid #999999;
        table-layout: fixed;
        width: 100%;
    }

    .key {
        color: blue;
    }

    .image-prompt {
        padding-top: 10px;
        padding-bottom: 10px;
    }

    .image {
        width: 100%;
    }
</style>
