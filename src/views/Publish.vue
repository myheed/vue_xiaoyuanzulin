<template lang="html">
  <!-- 在首页父组件发送http请求,后将数据通过props传递给子组件,可减少请求次数,减少服务器压力 -->

  <div class="index">
    <v-input></v-input>
    <v-footer></v-footer>
  </div>
</template>

<script>
import VHeader from '@/common/_header.vue'
import Header from '@/components/publish/header.vue'
import Input from '@/components/publish/input.vue'
import Uploader from '@/components/publish/img_uploader.vue'
import Swiper from '@/components/index/swiper.vue'
import Service from '@/components/index/service.vue'
import section3 from '@/components/index/section3.vue'
import Baseline from '@/common/_baseline.vue'
import Footer from '@/common/_footer.vue'
import index from '@/http/mock.js' //模拟数据

export default {
  components: {

    'vv-header': VHeader,
    'v-header': Header,
    'v-input': Input,
    'v-uploader':Uploader,
    'v-swiper': Swiper,
    'v-service': Service,
    'v-section3': section3,
    'v-baseline': Baseline,
    'v-footer': Footer
  },
  data() {
    return {
      datas: {
        section3:{},
        swiper:[]
      },
      loading: true
    }
  },

  beforeCreate() {
    this.$api({
      method: 'post',
      url: '/index'
    }).then((response) => {
      this.datas = response.data;
    }).catch(function(error) {
      alert(error)
    })
  }
}
</script>



<style lang="less" scoped>
.index {
    width: 100%;
    padding-bottom: 0vh;
    background-color: #F8FCFF;

}
</style>
