<template>
  <div class="menu-bar">
    <transition name="slide-up">
      <div :class="['menu-wrapper',isSettingShow || !ifTitleAndMenuShow ? 'hide-box-shadow' : '']" v-show="ifTitleAndMenuShow">
        <div class="icon-wrapper">
          <div class="icon icon-menu"></div>
        </div>
        <div class="icon-wrapper">
          <div class="icon icon-progress"></div>
        </div>
        <div class="icon-wrapper">
          <div class="icon icon-bright"></div>
        </div>
        <div class="icon-wrapper" @click="showSetting">
          <div class="icon icon-a">A</div>
        </div>
      </div>
    </transition>
    <transition name="slide-up">
      <div class="setting-wrapper" v-show="isSettingShow">
        <div class="setting-font-size">
          <div class="preview" :style="{fontSize:fontSizeList[0].fontSize+'px'}">A</div>
          <div class="font-select">
              <div class="line-row"></div>
              <div class="select-left" :style="{width:100/(fontSizeList.length*2)+'%'}"></div>
              <div class="select-right" :style="{width:100/(fontSizeList.length*2)+'%'}"></div>
              <div class="font-line">
                  <div
                    class="font-size-select"
                    v-for="(item,index) in fontSizeList"
                    @click="currenFontSize = item.fontSize"
                    :key="index">
                    <div :class="currenFontSize == item.fontSize ? 'pointer-wrapper' : 'line-pointer'">
                        <div class="pointer"></div>
                    </div>
                  </div>
              </div>
          </div>
          <div class="preview" :style="{fontSize:fontSizeList[fontSizeList.length-1].fontSize+'px'}">A</div>
        </div>
     </div>
    </transition>
  </div>
</template>
<script>
export default {
  props: {
    ifTitleAndMenuShow: {
      type: Boolean,
      default: false
    },
    fontSizeList: {
      type: Array
    }
  },
  data () {
    return {
      isSettingShow: false,
      currenFontSize: 12
    }
  },
  methods: {
    showSetting () {
      this.isSettingShow = true
    },
    hideSetting () {
      this.isSettingShow = false
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../assets/styles/global.scss';
.menu-bar{
  .menu-wrapper{
    position: absolute;
    bottom:0;
    left:0;
    width:100%;
    height:px2rem(48);
    box-shadow: 0 px2rem(-8) px2rem(8) #aaa;
    &.hide-box-shadow{
      box-shadow: none;
    }
    display: flex;
    z-index: 102;
    background:#fff;
    .icon-wrapper{
      flex:1;
      @include center;
      font-size: px2rem(24);
      cursor: pointer;
    }
  }
  .setting-wrapper{
    position: absolute;
    bottom:px2rem(48);
    left:0;
    width:100%;
    height:px2rem(60);
    box-shadow: 0 px2rem(-8) px2rem(8) #aaa;
    background:#fff;
    z-index:101;
    .setting-font-size{
      display: flex;
      height:100%;
      .preview{
        width:px2rem(60);
        background:#fff;
        height:100%;
        @include center
      }
      .font-select{
        flex:1;
        height:100%;
        background:#fff;
        position: relative;
        .select-left{
            position: absolute;
            top:0;
            left:-0.5px;
            height:100%;
            z-index: 103;
            background:#fff;
        }
        .select-right{
            position: absolute;
            top:0;
            right:-0.5px;
            height:100%;
            z-index: 103;
            background:#fff;
        }
        .line-row{
           position: absolute;
           top:calc(50% - 2px);
           left:0;
           width:100%;
           height:1px;
           border-bottom: 1px solid #ccc;
        }
        .font-line{
            width:100%;
            margin:auto;
            height:100%;
            border-bottom:1px solid #ccc;
            display: flex;
            .font-size-select{
                flex:1;
                @include center;
                .line-pointer{
                    border-right:1px solid #ccc;
                    width:0px;
                    height:8px;
                    overflow: hidden;
                }
                .pointer-wrapper{
                    position: relative;
                    z-index: 200;
                    width:10px;
                    height:10px;
                    border:1px solid #ccc;
                    border-radius:50%;
                    text-align: center;
                    line-height: 10px;
                    background:#fff;
                    .pointer {
                        width:100%;
                        height:100%;
                        border-radius: 50%;
                        border:2px solid #fff;
                        background:#aaa;
                        box-sizing: border-box;
                    }
                }
            }
        }
      }
    }
  }
}
</style>
