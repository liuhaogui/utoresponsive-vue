<template>
  <div class="albumPanel">
    <div v-show="loading">loading ...</div>
    <auto-responsive
        v-bind="options"
    >
      <draggable :list="arrayList" tag="div" class="list-group" draggable=".item" group="people" :sort="false">
        <a href="#" v-for="(item, index) in list" :style="getStyleList(item)" :class="`${item.w} album item`">
          <img class="a-cont j_ACont" src="images/a.jpg"/>
          <img class="a-cover" :src="item.src"/>
          <p class="a-mask">{{ index }}<i></i></p>
          <p class="a-layer">
            <span class="al-brand">{{ item.brand }}</span>
            <span class="al-title">{{ item.title }}</span>
            <span class="al-count">{{ item.count }}件商品</span>
          </p>
          <p class="a-more j_ALMore"></p>
        </a>
      </draggable>
    </auto-responsive>
    <Ribbon
        v-bind="ribbon"
    ></Ribbon>
  </div>
</template>
<script>
import draggable from 'vuedraggable';
import pkg from '../package';
import Utils from '../homepage/utils';
import AutoResponsive from '../src/autoresponsive.vue';

export default {
  name: 'app',
  components: {
    'auto-responsive': AutoResponsive,
    draggable
  },
  data() {
    return {
      loading: true,
      list: [],
      options: {
        itemMargin: 10,
        containerWidth: document.body.clientWidth,
        itemClassName: 'item',
        gridWidth: 100,
        transitionDuration: '.5'
      },
      ribbon: {
        text: 'Fork me on GitHub',
        linkUrl: pkg.repository.url,
        fixed: true,
        flat: true,
        classPrefix: pkg.name
      }
    };
  },
  beforeMount() {
    Utils.ajax('./data.json', d => {
      this.list = JSON.parse(d).data;
    });
  },
  mounted() {
    window.addEventListener('resize', () => {
      this.options.containerWidth = document.body.clientWidth;
    }, false);
  },
  methods: {
    getStyleList(i) {
      return {
        width: `${i.w === 'w1' ? 190 : 390}px`,
        height: `${i.w === 'w1' ? 240 : 490}px`
      };
    }
  },
  updated() {
    this.loading = false;
  }
};
</script>
<style lang="less">
@import '../assets/base.less';

::-webkit-scrollbar {
  width: 2px;
}

::-webkit-scrollbar-thumb {
  background: #000;
}

.albumPanel {
  position: relative;
  font-family: "Microsoft Yahei", arial;
  font-size: 12px;
  line-height: 1.5;
  text-align: center;
  margin: auto;
  margin-top: 5px;
  padding-bottom: 60px;
}

.albumPanel .aP-hd {
  text-align: left;
  color: #6d5c53;
}

.albumPanel .aP-hd i {
  background-position: -294px 0;
  display: inline-block;
  width: 18px;
  height: 17px;
  margin-bottom: -4px;
  margin-right: 5px;
}

.albumPanel .aP-hd b {
  background-position: -294px -30px;
  display: inline-block;
  width: 127px;
  height: 18px;
  color: transparent;
  margin-left: 15px;
  vertical-align: middle;
}

.albumPanel .aP-hd b s {
  display: none;
}

.albumPanel .aP-bd {
  position: relative;
  margin-left: -10px;
}

.albumPanel .album {
  display: block;
  overflow: hidden;
  text-decoration: none;
}

.albumPanel .album img {
  border: none;
}

.albumPanel .album .a-cont,
.albumPanel .album .a-cover {
  position: absolute;
  left: 0;
  top: 0;
  -webkit-transition: opacity 0.3s ease-in;
  -moz-transition: opacity 0.3s ease-in;
  -ms-transition: opacity 0.3s ease-in;
  -o-transition: opacity 0.3s ease-in;
  transition: opacity 0.3s ease-in;
}

.albumPanel .album .a-cover {
  opacity: 1;
}

.albumPanel .album .a-cont {
  opacity: 0;
}

.albumPanel .album:hover {
  text-decoration: none;
}

.albumPanel .album:hover .a-cover {
  opacity: 0;
}

.albumPanel .album:hover .a-cont {
  opacity: 1;
}

.albumPanel .album:hover .a-mask i {
  opacity: 1;
  -webkit-transition: opacity 0.2s ease-in 0.3s;
  -moz-transition: opacity 0.2s ease-in 0.3s;
  -ms-transition: opacity 0.2s ease-in 0.3s;
  -o-transition: opacity 0.2s ease-in 0.3s;
  transition: opacity 0.2s ease-in 0.3s;
}

.albumPanel .album .a-mask {
  position: absolute;
  height: 100%;
  width: 100%;
  top: 0;
  left: 0;
  margin: 0;
  padding: 0;
}

.albumPanel .album .a-mask i {
  display: block;
  opacity: 0;
  left: 50%;
  top: 40%;
  position: absolute;
}

.albumPanel .album .a-layer {
  position: absolute;
  left: 0;
  bottom: 0;
  height: 72px;
  width: 100%;
  margin: 0;
  padding: 0;
  background-image: -webkit-linear-gradient(top, rgba(240, 234, 228, 0.8) 0%, rgba(240, 234, 228, 1) 17%);
  background-image: -moz-linear-gradient(top, rgba(240, 234, 228, 0.8) 0%, rgba(240, 234, 228, 1) 17%);
  background-image: -ms-linear-gradient(top, rgba(240, 234, 228, 0.8) 0%, rgba(240, 234, 228, 1) 17%);
  background-image: -o-linear-gradient(top, rgba(240, 234, 228, 0.8) 0%, rgba(240, 234, 228, 1) 17%);
  background-image: linear-gradient(top, rgba(240, 234, 228, 0.8) 0%, rgba(240, 234, 228, 1) 17%);
  filter: progid:DXImageTransform.Microsoft.gradient(startcolorstr=#ccf0eae4,endcolorstr=#fff0eae4,gradientType=0);
  -webkit-transition: all 0.3s ease-in;
  -moz-transition: all 0.3s ease-in;
  -ms-transition: all 0.3s ease-in;
  -o-transition: all 0.3s ease-in;
  transition: all 0.3s ease-in;
}

.albumPanel .album .a-layer .al-brand,
.albumPanel .album .a-layer .al-title {
  -webkit-transition: all 0.5s ease-in 0.1s;
  -moz-transition: all 0.5s ease-in 0.1s;
  -ms-transition: all 0.5s ease-in 0.1s;
  -o-transition: all 0.5s ease-in 0.1s;
  transition: all 0.5s ease-in 0.1s;
}

.albumPanel .album .a-layer .al-brand {
  display: block;
  margin: 0;
  color: #6d5c53;
  text-decoration: none;
  line-height: 22px;
}

.albumPanel .album .a-layer .al-title {
  display: inline-block;
  color: #6d5c53;
  text-decoration: none;
  font-size: 16px;
  line-height: 26px;
  height: 26px;
  min-width: 80%;
  _width: 95%;
  white-space: nowrap;
  border-top: 1px dotted #a8a39f;
  overflow: hidden;
}

.albumPanel .album .a-layer .al-count {
  display: block;
  color: #beb5ae;
  text-decoration: none;
}

.albumPanel .album .a-more {
  display: none;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  margin: 0;
  padding: 0;
  height: 100%;
  font-size: 16px;
  line-height: 2.4;
  letter-spacing: .3em;
  font-family: arial;
  background-color: #dbdbdb;
  font-weight: bold;
  text-decoration: none;
  color: #000;
  z-index: 1;
  cursor: pointer;
  background-position: 0 0;
}

.albumPanel .album:hover .a-mask {
  background-color: transparent;
}

.albumPanel .album:hover .a-layer {
  background: none;
}

.albumPanel .album:hover .a-layer .al-brand,
.albumPanel .album:hover .a-layer .al-title {
  color: white;
}

.albumPanel .hasAlbums .album:last-child .a-more {
  display: block;
  -webkit-transition: all 0.2s ease-in 0s;
  -moz-transition: all 0.2s ease-in 0s;
  -ms-transition: all 0.2s ease-in 0s;
  -o-transition: all 0.2s ease-in 0s;
  transition: all 0.2s ease-in 0s;
}

.albumPanel .hasAlbums .album:last-child:hover .a-more {
  background-color: #999A99;
}

.albumPanel .hasAlbums .album-last-child .a-more {
  display: block;
  -webkit-transition: all 0.2s ease-in 0s;
  -moz-transition: all 0.2s ease-in 0s;
  -ms-transition: all 0.2s ease-in 0s;
  -o-transition: all 0.2s ease-in 0s;
  transition: all 0.2s ease-in 0s;
}

.albumPanel .hasAlbums .album-last-child:hover .a-more {
  background-color: #999A99;
}

.albumPanel .w1,
.albumPanel .w2 {
  position: absolute;
  -webkit-transform: translate(-450px, 999999px);
  -moz-transform: translate(-450px, 999999px);
  -ms-transform: translate(-450px, 999999px);
  -o-transform: translate(-450px, 999999px);
  transform: translate(-450px, 999999px);
  -ms-transform: none;
}

.albumPanel .w1 {
  width: 190px;
  height: 240px;
}

.albumPanel .w1 img {
  width: 190px;
}

.albumPanel .w1 .al-brand {
  padding-top: 3px;
}

.albumPanel .w1:hover .a-mask {
  background-image: -webkit-linear-gradient(top, rgba(0, 0, 0, 0) 45%, rgba(0, 0, 0, 0.1) 52%, rgba(0, 0, 0, 0.55) 67%, rgba(0, 0, 0, .7) 70%, rgba(0, 0, 0, 1) 81%);
  background-image: -moz-linear-gradient(top, rgba(0, 0, 0, 0) 45%, rgba(0, 0, 0, 0.1) 52%, rgba(0, 0, 0, 0.55) 67%, rgba(0, 0, 0, .7) 70%, rgba(0, 0, 0, 1) 81%);
  background-image: -ms-linear-gradient(top, rgba(0, 0, 0, 0) 45%, rgba(0, 0, 0, 0.1) 52%, rgba(0, 0, 0, 0.55) 67%, rgba(0, 0, 0, .7) 70%, rgba(0, 0, 0, 1) 81%);
  background-image: -o-linear-gradient(top, rgba(0, 0, 0, 0) 45%, rgba(0, 0, 0, 0.1) 52%, rgba(0, 0, 0, 0.55) 67%, rgba(0, 0, 0, .7) 70%, rgba(0, 0, 0, 1) 81%);
  background-image: linear-gradient(top, rgba(0, 0, 0, 0) 45%, rgba(0, 0, 0, 0.1) 52%, rgba(0, 0, 0, 0.55) 67%, rgba(0, 0, 0, .7) 70%, rgba(0, 0, 0, 1) 81%);
}

.albumPanel .w1:hover .a-mask i {
  background-position: -292px -60px;
  width: 78px;
  height: 78px;
  zoom: 0.5;
  -moz-transform: scale(0.5);
  margin-left: -40px;
  margin-top: -40px;
}

.albumPanel .w2 {
  width: 390px;
  height: 490px;
}

.albumPanel .w2 img {
  width: 390px;
}

.albumPanel .w2 .a-layer {
  padding: 28px 0 20px;
}

.albumPanel .w2 .a-layer .al-title {
  min-width: 60%;
}

.albumPanel .w2:hover .a-mask {
  background-image: -webkit-linear-gradient(top, rgba(0, 0, 0, 0) 53%, rgba(0, 0, 0, 0.65) 74%, rgba(0, 0, 0, 1) 81%);
  background-image: -moz-linear-gradient(top, rgba(0, 0, 0, 0) 53%, rgba(0, 0, 0, 0.65) 74%, rgba(0, 0, 0, 1) 81%);
  background-image: -ms-linear-gradient(top, rgba(0, 0, 0, 0) 53%, rgba(0, 0, 0, 0.65) 74%, rgba(0, 0, 0, 1) 81%);
  background-image: -o-linear-gradient(top, rgba(0, 0, 0, 0) 53%, rgba(0, 0, 0, 0.65) 74%, rgba(0, 0, 0, 1) 81%);
  background-image: linear-gradient(top, rgba(0, 0, 0, 0) 53%, rgba(0, 0, 0, 0.65) 74%, rgba(0, 0, 0, 1) 81%);
}

.albumPanel .w2:hover .a-mask i {
  background-position: -371px -56px;
  width: 170px;
  height: 170px;
  zoom: 0.5;
  -moz-transform: scale(0.5);
  margin-left: -86px;
  margin-top: -86px;
}

.albumPanel .aP-expand,
.albumPanel .aP-collapse {
  display: block;
  left: 0;
  bottom: 0;
  height: 60px;
  width: 100%;
  color: transparent;
  font-size: 12px;
  line-height: 36px;
  text-decoration: none;
  outline: none;
  background-color: rgba(255, 255, 255, 0.7);
  -webkit-transition: background-color .2s ease-in 0s, color .2s ease-in 0s;
  -moz-transition: background-color .2s ease-in 0s, color .2s ease-in 0s;
  -ms-transition: background-color .2s ease-in 0s, color .2s ease-in 0s;
  -o-transition: background-color .2s ease-in 0s, color .2s ease-in 0s;
  transition: background-color .2s ease-in 0s, color .2s ease-in 0s;
}

.albumPanel .aP-expand i,
.albumPanel .aP-collapse i {
  display: block;
  margin: auto;
  line-height: 25px;
  width: 50px;
  height: 50px;
  margin-top: -26px;
}

.albumPanel .aP-expand:hover,
.albumPanel .aP-collapse:hover {
  color: white;
  text-decoration: none;
  background-color: rgba(0, 0, 0, 0.5);
}

.albumPanel .aP-collapse {
  position: absolute;
  z-index: 1;
  opacity: 0;
}

.albumPanel .aP-collapse i {
  background-position: -201px -129px;
  width: 76px;
}

.albumPanel .aP-collapse:hover {
  color: transparent;
}

.albumPanel .aP-collapse:hover i {
  background-position: -201px -194px;
}

.albumPanel .aP-expand {
  position: fixed;
  background-color: rgba(238, 238, 238, 0.7);
}

.albumPanel .aP-expand i {
  background-position: -202px 0;
}

.albumPanel .aP-expand:hover {
  color: transparent;
}

.albumPanel .aP-expand:hover i {
  background-position: -202px -63px;
}

.fixedH {
  height: 290px;
  overflow: hidden;
}

.ie8 .albumPanel .al-count,
.ks-ie8 .albumPanel .al-count,
.ie9 .albumPanel .al-count,
.ks-ie9 .albumPanel .al-count {
  margin-top: -5px;
}

.ie8 .albumPanel .w1 .a-mask i,
.ks-ie8 .albumPanel .w1 .a-mask i {
  width: 39px;
  height: 39px;
  margin-top: 55px;
  margin-left: 55px;
}

.ie8 .albumPanel .w2 .a-mask i,
.ks-ie8 .albumPanel .w2 .a-mask i {
  width: 85px;
  height: 85px;
  margin-top: 110px;
  margin-left: 110px;
}

.ie6 .aP-expand,
.ks-ie6 .aP-expand,
.ie7 .aP-expand,
.ks-ie7 .aP-expand,
.ie8 .aP-expand,
.ks-ie8 .aP-expand,
.ie6 .aP-collapse,
.ks-ie6 .aP-collapse,
.ie7 .aP-collapse,
.ks-ie7 .aP-collapse,
.ie8 .aP-collapse,
.ks-ie8 .aP-collapse {
  text-indent: -99999px;
}

@media only screen and (-webkit-min-device-pixel-ratio: 2), only screen and (min-device-pixel-ratio: 2) {
  /* retina screen */
  .albumPanel .aP-hd b s {
    display: inline;
    color: #6d5c53;
    margin-left: 17px;
    text-decoration: none;
    background: white;
    padding: 2px 0;
  }

  .albumPanel .aP-collapse {
    color: #6d5c53;
  }

  .albumPanel .aP-collapse i {
    background-position: -201px -151px;
    margin-top: -5px;
  }

  .albumPanel .aP-collapse:hover {
    color: #fff;
  }

  .albumPanel .aP-collapse:hover i {
    background-position: -201px -216px;
  }

  .albumPanel .aP-expand {
    color: #6d5c53;
  }

  .albumPanel .aP-expand i {
    background-position: -202px -22px;
    margin-top: -5px;
  }

  .albumPanel .aP-expand:hover {
    color: #fff;
  }

  .albumPanel .aP-expand:hover i {
    background-position: -202px -84px;
  }
}

.a-mask {
  color: white;
  font-size: 120px;
}
</style>
