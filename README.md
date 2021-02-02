# 前言

vue多媒体轮播自动切换。结合swiper，视频自动轮播，且视频结束时自动切换下一个slide，图片则停留2s。分页器点击后也可以自动播放/停留完自动切换。



###### 使用

20210202更新：

由于swiper5不能兼容IE，需要兼容IE的可以用AutoplayNextSwiper-compatible.vue

vue-awesome-swiper得使用v2.6.7版本（同时swiper也需降级），详见https://github.com/surmon-china/vue-awesome-swiper/tree/v2.6.7



-----------------------------------------------------------------------------------------------------------------------------------------------



依赖vue-awesome-swiper，详见https://github.com/surmon-china/vue-awesome-swiper

图片自动切换时间按需在方法mediaNewsImgHandle内计时器里修改

对象内要有type字段判断是视频还是图片



