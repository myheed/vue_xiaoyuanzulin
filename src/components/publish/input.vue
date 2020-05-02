<template lang="html">
  <div style="background-color: #FFFFFF;">
    <mt-header title="发布物品"></mt-header>
    <mt-field label="物品名:" placeholder="请输入物品名" v-model="wupinName"></mt-field>
    <mt-field label="租金(元):" placeholder="请输入租金" type="number" v-model="zujin"></mt-field>
    <mt-field label="手机号" placeholder="请输入手机号" type="tel" v-model="phone"></mt-field>
    <mt-field label="商品介绍" placeholder="请输入商品介绍信息" type="textarea" rows="4" v-modal="introduction"></mt-field>
      <image-upload
        class="image_upload"
        url="https://tsesb.yunjuhe.com.cn/medicalServer/doctor/uploadServerImage"
        :touch-size="1"
        :multiple="true"
        field-name="serverImgFile"
        :max-count="10"
        @chooseImages="bindtap_chooseImages"
      />
    <!-- 图片预览 -->
      <img :src="image.src" alt="" v-for="(image, i) in images" @click="bingtap_preview(i)" />

      <image-preview style="z-index:200" :images="preImages" v-model="index" :numIsShow="true" :deleteIsShow="true" @delete="bindtap_delete" />
      <!-- <mt-field type="button"><mt-button type="default" size="large"></mt-button></mt-field> -->
    <mt-button type="primary" style="width: 100%;margin-top: 4vw;" @click.native="bindtap_upload">发布</mt-button>
  </div>
</template>
<script>
import { ImageUpload, ImagePreview } from 'vue-image-upload-preview';
import { Lazyload } from 'mint-ui';
import { Field, Button } from 'mint-ui';
export default {
  components: {
    'mt-field': Field,
    'image-preview': ImagePreview,
    'image-upload': ImageUpload
  },
  computed: {
    // 预览图片路径
    preImages() {
      return this.images.map(v => {
        return v.src;
      });
    }
  },
  methods: {
    bindtap_chooseImages(res) {
      if (Array.isArray(res)) {
        this.images = this.images.concat(res);
      } else {
        console.log(res);
      }
    },

    /**
     *  绑定函数 -- 删除图片
     */
    bindtap_delete() {
      this.images = this.images.filter((v, i) => {
        return this.index != i;
      });
    },

    /**
     *  绑定函数 -- 预览图片
     */
    bingtap_preview(i) {
      this.index = i;
    },

    /**
     *  绑定函数 -- 取消预览
     */
    bingtap_hiddenImg() {
      this.index = -1;
    },

    bindtap_upload() {
      let data = {
        wupinName: this.wupinName,
        zujin: this.zujin,
        phone: this.phone,
        introduction: this.introduction,
        images: this.images,
      };
      this.$api({
        method: 'post',
        url: '/index',
        data
      }).then((response) => {
        console.log(response)
        this.datas = response.data;
      }).catch(error => {
          console.log(err);
      })
    }
  },
  data() {
    return {
      wupinName: '',
      zujin: '',
      phone: '',
      introduction: '',
      msg: 'Welcome to Your Vue.js App',
      images: [],
      index: -1
    };
  }
};
</script>

<style lang="less" scoped>
@import '../../assets/fz.less';
@import '../../assets/index/style.css';
* {
  padding: 0;
  margin: 0;
}
img {
  height: 60px;
  width: 60px;
}

.image_upload {
  float: left;
  height: 60px;
  width: 60px;
  background-image: url('../../assets/uploader.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
  -moz-background-size: 100% 100%;
}
</style>
