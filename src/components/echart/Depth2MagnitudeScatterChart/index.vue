<template>
    <div>
        <Chart :cdata="cdata" />
    </div>
</template>

<script>
import Chart from './chart.vue'
import { csvParse } from 'd3-dsv'
export default {
    data() {
        return {
            cdata: {
                data: []
            }
        }
    },
    components: {
        Chart,
    },
    mounted() {
        this.getData();
    },
    methods: {
        getData() {
            this.$axios
                .get("/震级深度.csv")
                .then(res => {
                    var csv = csvParse(res.data, (d) => {
                        return {
                            magnitude: +d.zhenji,
                            depth: +d.fdepth
                        };
                    });
                    var obj = csv;
                    var arr = [];
                    for (var i in obj) {
                        var item = [];
                        item = Object.values(obj[i]);
                        arr.push(item);
                    }
                    this.cdata.data = arr;
                    //console.log(csv);
                });
        }
    }
}
</script>
