<template>
    <ag-grid-vue class="ag-fresh grid"
                 :gridOptions="gridOptions"
                 :rowData="rowData"
                 :rowClicked="onRowClicked"
                 :rowDataChanged="onRowDataChanged">
    </ag-grid-vue>
</template>

<script>
    import Vue from "vue";
    import {AgGridVue} from "ag-grid-vue";
    import 'whatwg-fetch'

    import SliderFilter from './SilderFilter.vue';

    export default {
        name: 'munro-grid',
        data () {
            return {
                gridOptions: null,
                rowData: null
            }
        },
        components: {
            AgGridVue
        },
        methods: {
            loadRowData() {
                fetch('/static/munros.json')
                    .then((response) => {
                        return response.json()
                    })
                    .then((json) => {
                        this.rowData = json;
                    });
            },
            createColDefs() {
                return [
                    {headerName: "Hill Name", field: "hillname", width: 225, suppressSizeToFit: true},
                    {headerName: "Grid Reference", field: "gr6"},
                    {
                        headerName: "Height (m)",
                        field: "height",
                        filterFramework: SliderFilter,
                        filterParams: {
                            min: 900,
                            max: 1500,
                            step: 100,
                            initialValue: 1500
                        }
                    },
                    {headerName: "Latitude", field: "latitude"},
                    {headerName: "Longitude", field: "longitude"}
                ];
            },
            onRowClicked(params) {
                this.$emit("munroSelected", params.node.data)
            },
            onRowDataChanged() {
                Vue.nextTick(() => {
                        this.gridOptions.api.sizeColumnsToFit();
                    }
                );
            }
        },
        created() {
            this.gridOptions = {
                enableFilter:true
            };
            this.gridOptions.columnDefs = this.createColDefs();
            this.loadRowData();
        }
    }
</script>

<style scoped>
    .grid {
        height: 255px;
    }
</style>
