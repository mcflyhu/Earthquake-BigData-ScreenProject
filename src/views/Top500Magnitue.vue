<template>
  <div id="Top500Magnitude">
    <div class="bg-color-black">
      <div class="d-flex pt-2 pl-2">
        <span>
          <icon name="chart-line" class="text-icon"></icon>
        </span>
        <div class="d-flex">
          <span class="fs-xl text mx-2">震级排行榜</span>
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
        header: ['时间', '地区', '震级'],
        data: [],
        rowNum: 10, //表格行数
        headerHeight: 35,
        headerBGC: '#0f1325', //表头
        oddRowBGC: '#0f1325', //奇数行
        evenRowBGC: '#27408B', //偶数行
        index: true,
        columnWidth: [50, 140, 200, 50],
        align: ['center']
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
$box-height: 610px;
$box-width: 500px;

#Top500Magnitude {
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
      width: 480px;
      height: 540px;
    }
  }
}
</style>

<!--<template>
  <div id="Top500Magnitude">
    <div class="bg-color-black">
      <div class="d-flex pt-2 pl-2">
        <span>
          <icon name="chart-line" class="text-icon"></icon>
        </span>
        <div class="d-flex">
          <span class="fs-xl text mx-2">全球震级排行榜</span>
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
        header: ['时间', '地区', '震级'],
        rowNum: 5, // 表行数,
        headerHeight: 35,
        headerBGC: '#0f1325', //表头
        oddRowBGC: '#0f1325', //奇数行
        evenRowBGC: '#000099', //偶数行
        index: true,
        columnWidth: [100, 100, 50],
        align: ['center'],
        waitTime: 3000,
        data: [
          ['行1列1', '行1列2', '行1列3'],
          ['行2列1', '行2列2', '行2列3'],
          ['行3列1', '行3列2', '行3列3'],
          ['行4列1', '行4列2', '行4列3'],
          ['行5列1', '行5列2', '行5列3'],
          ['行6列1', '行6列2', '行6列3'],
          ['行7列1', '行7列2', '行7列3'],
          ['行8列1', '行8列2', '行8列3'],
          ['行9列1', '行9列2', '行9列3'],
          ['行10列1', '行10列2', '行10列3']
        ],
      }
    }
  },
  created() {
    //this.getData();
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
          console.log(this.config.data);
          //console.log(csv);
        });
    }
  }
}
</script>


<style lang="scss" scoped>
$box-height: 410px;
$box-width: 300px;

#Top500Magnitude {
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
      width: 270px;
      height: 340px;
    }
  }
}
</style>
-->