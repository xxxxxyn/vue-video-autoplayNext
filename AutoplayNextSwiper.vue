<template>
  <div class="test">
    <div class="autoplay">
      <swiper :options="swiperOption" ref="videoSwiper">
        <swiper-slide v-for="( item , index ) in mediaNews" :key="index">
          <video v-if="item.type===1"
                 :src="item.url"
                 controls
                 muted
                 @ended="endVideo(index)"
                 class="multimedia"
          ></video>
          <img v-else :src="item.url" class="multimedia">
        </swiper-slide>
        <div class="swiper-pagination" v-for="item in mediaNews" :key="index" slot="pagination"></div>
      </swiper>
    </div>
  </div>
</template>

<script>
  export default {
    name: "AutoplayNextSwiper",
    data() {
      return {
        swiperOption: {
          speed: 1000,
          loop: false,
          observer: true,
          observeParents: true,
          autoplayDisableOnInteraction: false,
          allowTouchMove: false,
          pagination: {
            el: ".swiper-pagination",
            clickable: true,
          },
          on: {
            click: () => {
            },
            //初始化时控制第一个slide切换
            init: () => {
              this.initHandle()
            },
            slideChangeTransitionEnd: () => {
              this.slideChangeTransitionEndHandle()
            }
          }
        },
        mediaNews: [
                //1为视频类0为图片类
          {url: require('../../assets/img/default3.jpg'), type: 0},
          {url: require('../../assets/temp/video1.mp4'), type: 1},
          {url: require('../../assets/temp/video1.mp4'), type: 1},
          {url: require('../../assets/img/default3.jpg'), type: 0},
        ],
      }
    },
    methods: {
      mediaNewsImgHandle(swiper) {
        if (swiper.activeIndex < this.mediaNews.length - 1) {
          setTimeout(function () {
            swiper.slideNext()
          }, 2000)
        } else {
          setTimeout(function () {
            swiper.slideTo(0, 1000)
          }, 2000)
        }
      },
      initHandle() {
        let that = this
        setTimeout(function () {
          let swiper = that.$refs.videoSwiper.$swiper;
          console.log(swiper)
          if (that.mediaNews[0].type === 0) {
            that.mediaNewsImgHandle(swiper)
          } else {
            document.getElementsByClassName('multimedia')[0].play()
          }
        },200)

      },
      slideChangeTransitionEndHandle() {
        let that = this
        let swiper = that.$refs.videoSwiper.$swiper;
        if (this.mediaNews[swiper.activeIndex].type === 0) {
          this.mediaNewsImgHandle(swiper)
        } else {
          document.getElementsByClassName('multimedia')[swiper.activeIndex].play()
        }
      },
      endVideo(index) {
        let swiper = this.$refs.videoSwiper.$swiper;
        if (index === swiper.activeIndex) {
          if (swiper.activeIndex < this.mediaNews.length - 1) {
            swiper.slideNext()
            if (this.mediaNews[swiper.activeIndex].type === 1) {
              document.getElementsByClassName('multimedia')[swiper.activeIndex].play()
            } else {
            }
          } else {
            swiper.slideTo(0, 1000)
            document.getElementsByClassName('multimedia')[swiper.activeIndex].play()
          }
        }

      },
    },
  }
</script>

<style lang="less" scoped>
  .test {
    .autoplay {
      .multimedia {
        width: 42vw;
        height: 42vh;
      }

      /deep/ .swiper-container {
        width: 42vw;
        height: 42vh;
        background: #0c0000;
      }

      /deep/ .swiper-pagination {
        z-index: 123;
        left: 16vw;
      }

      /deep/ .swiper-pagination-bullet {
        width: 20px;
        height: 20px;
        background: #fff;
        border: solid 2px #0c8fcf;
      }

      /deep/ .swiper-pagination-bullets {
        /*width: 200px;
        top: 120px;*/
      }
    }
  }


</style>
