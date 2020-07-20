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
        <swiper-item v-for="item in banner" :key="item._id">
          <navigator :url="`/pages/lesson/index?Id=${item.aid}`">
            <image mode="scaleToFill" :src="item.cover"></image>
          </navigator>
        </swiper-item>
      </swiper>
    </view>
    <!-- icons -->
    <view class="icons">
      <view class="item">
        <image mode="scaleToFill" :src="item.imgUrl"></image>
        <text class="title"></text>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      banner: []
    };
  },
  onLoad() {},
  mounted() {
    this.init();
  },
  methods: {
    init() {
      uni.request({
        url: "https://opser.api.dgtle.com/v1/carousel/2",
        data: {},
        header: {},
        success: res => {
          this.banner = res.data;
        }
      });
    }
  }
};
</script>

<style lang="scss" scoped>
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
