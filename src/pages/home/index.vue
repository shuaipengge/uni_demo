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
      <view class="item-icon" v-for="item in icons" :key="item.id">
        <image mode="scaleToFill" :src="item.url"></image>
        <text class="title">{{ item.title }}</text>
      </view>
    </view>

    <view class="body-content" v-for="item in index.items" :key="item._id">
      <!-- 兴趣动态  type = 4 -->
      <view class="dongtai" v-if="item.type === 4">
        <view class="images" v-if="item.imgs_url.length > 1">
          <image mode="aspectFill" :src="item.imgs_url[0]"></image>
          <image mode="aspectFill" :src="item.imgs_url[1]"></image>
        </view>
        <view class="images-one" v-else>
          <image mode="aspectFill" :src="item.imgs_url[0]"></image>
        </view>
        <view class="title">{{ item.summary }}</view>
        <view class="zan">
          <view class="left"
            >👍 {{ item.liketimes }} 😃 {{ item.commentnum }}</view
          >
          <view class="right">{{ item.author.username }} · 兴趣动态</view>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      banner: [],
      icons: [
        { id: 1, title: "点评", url: "../../static/icon/shoucang.png" },
        { id: 2, title: "文章", url: "../../static/icon/wenzhang.png" },
        { id: 3, title: "鲸闻", url: "../../static/icon/jingtu.png" },
        { id: 4, title: "活动", url: "../../static/icon/huodong.png" }
      ],
      index: []
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
      uni.request({
        url: "https://opser.api.dgtle.com/v1/app/index?page=1",
        data: {},
        header: {},
        success: res => {
          this.index = res.data;
        }
      });
    }
  }
};
</script>

<style lang="scss" scoped>
.page {
  @extend .content;
  @extend .bgc;
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

  .icons {
    display: flex;
    width: 100%;
    justify-content: space-around;
    margin: 10px 0;
    .item-icon {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      image {
        width: 40px;
        height: 40px;
      }
      text {
        font-size: 12px;
        color: #2e2e2e;
      }
    }
  }

  .body-content {
    margin: 0 20px 15px 20px;
    background-color: #fff;
    box-shadow: 0 0 60px 0 hsla(0, 0%, 89%, 0.5);
    border-radius: 12px;
    .dongtai {
      padding: 10px;
      .images {
        image {
          width: 295rpx;
          height: 295rpx;
          margin: 10px 5px;
          border-radius: 5px;
        }
      }
      .images-one {
        image {
          width: 610rpx;
          height: 250rpx;
          margin: 10px 5px;
          border-radius: 5px;
        }
      }
      .title {
        font-size: 18px;
        color: #2d3f56;
        text-align: left;
        line-height: 22px;
        @extend .text-hidden;
      }
      .zan {
        margin-top: 5px;
        display: flex;
        justify-content: space-between;
        font-size: 13px;
        color: #bcbcbc;
      }
    }
  }
}
</style>
