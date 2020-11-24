<template>
  <div class="ebook">
    <titleBar :ifTitleAndMenuShow="ifTitleAndMenuShow"></titleBar>
    <div class="read-wrapper">
      <div id="read">
        <div class="mask">
          <div class="left" @click="prevPage"></div>
          <div class="center" @click="toggleTitleAndMenu"></div>
          <div class="right" @click="nextPage"></div>
        </div>
      </div>
    </div>
    <menuBar ref="menubar"
     :fontSizeList="fontSizeList"
     :ifTitleAndMenuShow="ifTitleAndMenuShow"></menuBar>
  </div>
</template>

<script>
import titleBar from './components/titleBar.vue'
import menuBar from './components/menuBar.vue'
import Epub from 'epubjs'
let DOWNLOAD_URL = '/static/1qinkan.net.epub'
export default {
  data () {
    return {
      book: null,
      rendition: null,
      ifTitleAndMenuShow: false,
      fontSizeList: [
        {fontSize: 12},
        {fontSize: 14},
        {fontSize: 16},
        {fontSize: 18},
        {fontSize: 20},
        {fontSize: 22},
        {fontSize: 24}
      ]
    }
  },
  components: {
    titleBar,
    menuBar
  },
  mounted () {
    this.showEpub()
  },
  methods: {
    toggleTitleAndMenu () {
      this.ifTitleAndMenuShow = !this.ifTitleAndMenuShow
      if (!this.ifTitleAndMenuShow) {
        this.$refs.menubar.hideSetting()
      }
    },
    /* 电子书的解析和渲染 */
    showEpub () {
      /* 1.生成Book */
      this.book = new Epub(DOWNLOAD_URL)
      console.log(this.book)
      /* 2.生成Rendition，通过Book.renderTo */
      this.rendition = this.book.renderTo('read', {
        width: window.innerWidth,
        height: window.innerHeight
      })
      /* 3.通过Rendition.display渲染电子书 */
      this.rendition.display()
    },
    /* 回到上一页 */
    prevPage () {
      if (this.rendition) {
        this.rendition.prev()
      }
    },
    /* 下一页 */
    nextPage () {
      if (this.rendition) {
        this.rendition.next()
      }
    }
  }
}
</script>

<style lang="scss" scoped>
@import './assets/styles/global.scss';
.ebook{
  position: relative;
  overflow-y: hidden;
  overflow-x: hidden;
  .read-wrapper{
    #read{
      .mask{
        position: absolute;
        top:0;
        left:0;
        width:100%;
        height:100%;
        display: flex;
        z-index:100;
        .left{
          flex:0 px2rem(100);
        }
        .center{
          flex:1;
        }
        .right{
          flex:0 px2rem(100);
        }
      }
    }
  }
}
</style>
