<template>
  <transition name="slide-down">
    <div class="title-wrapper" v-show="ifTitleAndMenuShow">
      <div class="left">
        <div class="icon-back icon"></div>
      </div>
      <div class="right">
        <div class="icon-wrapper">
          <div class="icon-cart icon"></div>
        </div>
        <div class="icon-wrapper">
          <div class="icon-person icon"></div>
        </div>
        <div class="icon-wrapper">
          <div class="icon-more icon"></div>
        </div>
      </div>
    </div>
  </transition>
</template>
<script>
export default {
  props: {
    ifTitleAndMenuShow: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../assets/styles/global.scss';
.title-wrapper{
  position: absolute;
  top:0;
  left:0;
  width:100%;
  height:px2rem(48);
  box-shadow: 0 px2rem(8) px2rem(8) #aaa;
  display: flex;
  z-index: 101;
  background:#fff;
  .left{
    flex:0 px2rem(60);
    @include center;
  }
  .right{
    flex:1;
    display:flex;
    justify-content: flex-end;
    .icon-wrapper{
      width:px2rem(50);
      font-size: 24px;
      cursor: pointer;
      @include center;
    }
  }
}
</style>
