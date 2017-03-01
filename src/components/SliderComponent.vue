<template>
    <span class="slider">
        <input type="range" :min="min" :max="max" :step="step" :value="value" @input="onSliderChanging" @change="onSliderChanged" /> {{ value }}
    </span>
</template>

<script>
    export default {
        name: 'slider',
        props: {
            min: {
                type: Number,
                default: 0
            },
            max: {
                type: Number,
                default: 100
            },
            step: {
                type: Number,
                default: 1
            },
            initialValue: {
                type: Number,
                default: 0
            },
        },
        data () {
            return {
                value: this.initialValue,
                currentTimout: null
            }
        },
        methods: {
            // for updates while the user is still actively dragging
            onSliderChanging($event) {
                this.value = $event.target.value;
            },
            // for when the user has chosen a value
            onSliderChanged($event) {
                this.value = $event.target.value;
                this.$emit("valueChanged", this.value)
            }
        }
    }
</script>

<style scoped>
    .slider {
        border: 1px solid lightgrey;
        padding-top: 4px;
        padding-right: 4px;
        z-index: 1;
    }
</style>
