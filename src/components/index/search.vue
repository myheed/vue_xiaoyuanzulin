<template lang="html">
  <div class="page-search">
      <form action="" target="frameFile" οnsubmit="return false">
         <mt-search v-model="commodityName" cancel-text="取消"  placeholder="搜索" @keyup.enter.native="loadListData"></mt-search>
      </form>
      <iframe name='frameFile' style="display: none;"></iframe>
  </div>
</template>

<script>
import { Search} from 'mint-ui';
export default {
  components:Search,
}
</script>

<style lang="less" scoped>
@import '../../assets/fz.less';
@import '../../assets/index/style.css';
  .searchWrap {
    margin: 5px 8px;
    background: #fff;
  }
  .mint-searchbar{
    padding:5px 5px 0 5px;
    box-sizing: border-box
  }
  .mint-search{
    height: 7vh;
  }
</style>
