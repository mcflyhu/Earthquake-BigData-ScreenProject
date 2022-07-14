<template>
  <div>
    <Chart :cdata="cdata" />
  </div>
</template>

<script>
import Chart from './chart.vue';
import { csvParse } from 'd3-dsv'
export default {
  data() {
    return {
      cdata: []
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
        .get("/地区次数.csv")
        .then(res => {
          var csv = csvParse(res.data, (d) => {
            return {
              name: d.area,
              value: +d.count
            };
          });
          this.cdata = csv;
          //console.log(this.cdata);
          //console.log(csv);
        });
    }
  }
}
</script>

<style lang="scss" scoped>
</style>