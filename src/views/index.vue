<template>
  <div id="index" ref="appRef">
    <div class="bg">
      <dv-loading v-if="loading">Loading...</dv-loading>
      <div v-else class="host-body">
        <div class="d-flex jc-center">
          <dv-decoration-10 class="dv-dec-10" />
          <div class="d-flex jc-center">
            <dv-decoration-8 class="dv-dec-8" :color="decorationColor" />
            <div class="title">
              <span class="title-text">全球地震大数据平台</span>
              <dv-decoration-6 class="dv-dec-6" :reverse="true" :color="['#50e3c2', '#67a1e5']" />
            </div>
            <dv-decoration-8 class="dv-dec-8" :reverse="true" :color="decorationColor" />
          </div>
          <dv-decoration-10 class="dv-dec-10-s" />
        </div>

        <!-- 第二行 -->
        <div class="d-flex jc-between px-2">
          <div class="d-flex aside-width">
            <div class="react-left ml-4 react-l-s">
              <span class="react-left"></span>
              <span class="text">项目成员：王朕 | 陈艺鑫 | 陈涛 | 胡千越</span>
            </div>
          </div>
          <div class="d-flex aside-width">
            <div class="react-right bg-color-blue mr-3">
              <span class="text fw-b">数据来源：中国地震台网|USGS</span>
            </div>
            <div class="react-right mr-4 react-l-s">
              <span class="react-after"></span>
              <span class="text">{{ dateYear }} {{ dateWeek }} {{ dateDay }}</span>
            </div>
          </div>
        </div>

        <div class="body-box">
          <!-- 第三行数据 -->
          <div class="content-box">
            <div>
              <dv-border-box-10>
                <CenterLeft />
              </dv-border-box-10>
            </div>
            <!-- 中间 
            <div>
              <center />
            </div>
            -->
            <!-- 中间 -->
            <div>
              <dv-border-box-8>
                <EarthquakeFre_CN />
              </dv-border-box-8>
            </div>
            <div>
              <dv-border-box-13>
                <Top500Magnitue />
              </dv-border-box-13>
            </div>
          </div>

          <!-- 第四行数据 -->
          <div class="bottom-box">
            <dv-border-box-13 style="height:330px">
              <AreaCount />
            </dv-border-box-13>
            <dv-border-box-12 style="height:330px">
              <bottomRight />
            </dv-border-box-12>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import drawMixin from "../utils/drawMixin";
import { formatTime } from '../utils/index.js'
//import centerLeft1 from './centerLeft1'
//import centerLeft2 from './centerLeft2'
//import centerRight1 from './centerRight1'
//import centerRight2 from './centerRight2'
//import center from './center'
//import bottomLeft from './bottomLeft'
import bottomRight from './bottomRight'
import Top500Magnitue from "./Top500Magnitue"
import EarthquakeFre_CN from "./EarthquakeFre_CN"
import AreaCount from "./AreaCount";
import CenterLeft from "./centerLeft"
//import Top500Depth from "./Top500Depth";
//import ScrollBoradRank from "./ScrollBoradRank";

export default {
  mixins: [drawMixin],
  data() {
    return {
      timing: null,
      loading: true,
      dateDay: null,
      dateYear: null,
      dateWeek: null,
      weekday: ['周日', '周一', '周二', '周三', '周四', '周五', '周六'],
      decorationColor: ['#568aea', '#000000']
    }
  },
  components: {
    //centerLeft1,
    //centerLeft2,
    //centerRight1,
    //centerRight2,
    //center,
    //bottomLeft,
    bottomRight,
    Top500Magnitue,
    EarthquakeFre_CN,
    AreaCount,
    CenterLeft
  },
  mounted() {
    this.timeFn()
    this.cancelLoading()
  },
  beforeDestroy() {
    clearInterval(this.timing)
  },
  methods: {
    timeFn() {
      this.timing = setInterval(() => {
        this.dateDay = formatTime(new Date(), 'HH: mm: ss')
        this.dateYear = formatTime(new Date(), 'yyyy-MM-dd')
        this.dateWeek = this.weekday[new Date().getDay()]
      }, 1000)
    },
    cancelLoading() {
      setTimeout(() => {
        this.loading = false
      }, 500)
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../assets/scss/index.scss';
</style>
