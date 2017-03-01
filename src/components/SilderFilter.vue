<template>
    <slider :min="min" :max="max" :step="step" :initialValue="initialValue" @valueChanged="filterValueChanged"></slider>
</template>

<script>
    import Vue from "vue";
    import Slider from './SliderComponent.vue';

    export default Vue.extend({
        name: 'slider-filter',
        data() {
            return {
                value: 0,
                valueGetter: null,
                min: null,
                max: null,
                step: null,
                initialValue: null
            }
        },
        components: {
            Slider
        },
        methods: {
            isFilterActive() {
                return true;
            },

            doesFilterPass(params){
                return this.valueGetter(params.node) <= this.value;
            },

            getModel() {
                return {value: this.value};
            },

            setModel(model) {
                this.value = model.value;
            },

            filterValueChanged(value) {
                this.value = value;
                this.params.filterChangedCallback();
            }
        },
        created() {
            this.valueGetter = this.params.valueGetter;

            this.min = this.params.min;
            this.max = this.params.max;
            this.step = this.params.step;
            this.initialValue = this.params.initialValue;
        }
    })
</script>
