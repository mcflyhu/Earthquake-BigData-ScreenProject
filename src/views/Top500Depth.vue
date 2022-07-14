<template>
  <div id="Top500Depth">
    <div class="bg-color-black">
      <div class="d-flex pt-2 pl-2">
        <span>
          <icon name="chart-line" class="text-icon"></icon>
        </span>
        <div class="d-flex">
          <span class="fs-xl text mx-2">全球震源深度排行</span>
        </div>
      </div>
      <div class="d-flex jc-center body-box">
        <dv-scroll-board class="dv-scr-board" :config="config" />
      </div>
    </div>
  </div>
</template>

<script>
import { csvParse } from 'd3-dsv';

export default {
  data() {
    return {
      config: {
        header: ['时间', '地区', '震源深度'],
        data: [],
        rowNum: 7, //表格行数
        headerHeight: 35,
        headerBGC: '#0f1325', //表头
        oddRowBGC: '#473C8B', //奇数行
        evenRowBGC: '#EE799F', //偶数行
        index: true,
        columnWidth: [50, 140, 200, 80],
        align: ['center', 'center', 'center', 'center']
      }
    }
  },
  created() {
    this.getData();
  },
  methods: {
    getData() {
      this.$axios
        .get("/Top500Magnitude.csv")
        .then(res => {
          var csv = csvParse(res.data, (d) => {
            return {
              time: d.time,
              area: d.place,
              magnitude: d.zhenji
            };
          });
          var obj = csv;
          var arr = [];
          for (var i in obj) {
            var item = [];
            item = Object.values(obj[i]);
            arr.push(item);
          }

          this.config.data = arr;
          this.config = { ...this.config };
          //console.log(this.config.data);
          //console.log(csv);
        });
    }
  }
}
</script>

<style lang="scss" scoped>
$box-height: 410px;
$box-width: 500px;

#Top500Depth {
  padding: 16px;
  padding-top: 20px;
  height: $box-height;
  width: $box-width;
  border-radius: 5px;

  .bg-color-black {
    height: $box-height - 30px;
    border-radius: 10px;
  }

  .text {
    color: #c3cbde;
  }

  .body-box {
    border-radius: 10px;
    overflow: hidden;

    .dv-scr-board {
      width: 500px;
      height: 340px;
    }
  }
}
</style>

