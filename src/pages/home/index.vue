<template>
  <view class="page">
    <!-- 轮播图 -->
    <view class="lunbo">
      <swiper
        class="swiper"
        indicator-dots
        autoplay
        interval="2000"
        duration="500"
      >
        <swiper-item v-for="item in banner" :key="item.id" :src="item.imgUrl">
          <image mode="scaleToFill" :src="item.imgUrl"></image>
        </swiper-item>
      </swiper>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      banner: [
        {
          id: 1,
          imgUrl:
            "http://p1.music.126.net/3Oz3JpYirDfQOmzgERgGJw==/109951165152149436.jpg"
        },
        {
          id: 2,
          imgUrl:
            "http://p1.music.126.net/GGvIzHA3nhVD0DI0oXXYzg==/109951165152401266.jpg"
        },
        {
          id: 3,
          imgUrl:
            "http://p1.music.126.net/KqqbRg-D-FYdpQX-NZ3bTQ==/109951165152205791.jpg"
        },
        {
          id: 4,
          imgUrl:
            "http://p1.music.126.net/a5lQUWV7cfIyN0hXZQF_3w==/109951165152417733.jpg"
        }
      ]
    };
  },
  onLoad() {},
  methods: {}
};
</script>

<style lang="scss">
.page {
  @extend .content;
  // @extend .bgc;
  .lunbo {
    width: 715rpx;
    height: 150px;
    margin: 10px;
    border-radius: 10px;
    overflow: hidden;
    image {
      width: 715rpx;
      height: 150px;
    }
  }
}
</style>
