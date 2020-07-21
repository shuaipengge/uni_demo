<template>
  <view class="page">
    <!-- 封面图 -->
    <view class="cover">
      <image mode="widthFix" :src="lesson.cover"></image>
    </view>

    <view class="content-text">
      <!-- 作者信息 -->
      <view class="author">
        <image mode="scaleToFill" :src="lesson.author.avatar_path"></image>
        <text>{{ lesson.author.username }}</text>
      </view>

      <!-- 文章标题 -->
      <view class="title">
        <text>{{ lesson.title }}</text>
      </view>

      <!-- 文章日期 -->
      <view class="date" v-if="lesson.relativeTime">
        <text>{{ lesson.relativeTime }} · 来自文章</text>
      </view>

      <!-- 文章内容 -->
      <view class="content" v-if="lesson.content">
        <u-parse :content="lesson.content"></u-parse>
      </view>

      <!-- 点赞 -->
      <view class="likelist">
        <view class="like">
          <view class="iconfont icon-icon_love"></view>
        </view>
        <text v-if="lesson.liketimes">{{ lesson.liketimes }} 人已赞</text>
        <view class="head-img" v-if="lesson.likelist">
          <!-- aspectFill 完整显示图片 保持纵横比 -->
          <image
            mode="aspectFill"
            v-for="item in lesson.likelist"
            :key="item.id"
            :src="item.avatar_path"
          ></image>
          <view class="last-head"> +{{ lesson.liketimes - 5 }}</view>
        </view>
      </view>

      <!-- 猜你喜欢 -->
      <view class="you-like">
        <text>可能你还会喜欢</text>
      </view>
      <navigator
        class="perhaps_like"
        v-for="item in lesson.perhaps_like"
        :key="item.id"
        :url="`/pages/lesson/index?Id=${item.id}`"
      >
        <view class="left">
          <image mode="aspectFill" :src="item.cover"></image>
        </view>

        <view class="righ">
          <view class="like-title">{{ item.title }}</view>
          <view class="like-username">{{ item.author.username }}</view>
        </view>
      </navigator>

      <!-- 评论区 -->
    </view>
  </view>
</template>

<script>
import uParse from "@/components/u-parse/u-parse.vue";

export default {
  components: {
    uParse
  },
  data() {
    return {
      id: null,
      lesson: null
    };
  },
  onLoad: function(option) {
    this.id = option.Id;
  },
  mounted() {
    this.getLesson();
  },
  methods: {
    getLesson() {
      console.log(this.id);
      uni.request({
        url: `https://opser.api.dgtle.com/v1/article/view/${this.id}`,
        data: {},
        header: {},
        success: res => {
          this.lesson = res.data;
        }
      });
    }
  }
};
</script>

<style lang="scss" scoped>
@import url("@/components/u-parse/u-parse.css");
@import url("../../static/iconfont/iconfont.css");

.page {
  @extend .content;
  // @extend .bgc;
  .cover {
    width: 100%;
    image {
      width: 100%;
    }
  }
  .content-text {
    padding: 0 22px;
    .author {
      display: flex;
      flex-direction: row;
      align-items: center;
      width: 680rpx;
      height: 40px;
      margin: 20px 0;
      image {
        width: 40px;
        height: 40px;
        border-radius: 50%;
      }
      text {
        margin-left: 9px;
        color: #435771;
        font-size: 14px;
      }
    }
    .title {
      font-size: 22px;
      color: #0f2540;
      margin-bottom: 12px;
    }
    .date {
      text {
        color: #c6c6c6;
        font-size: 12px;
      }
    }
    .content {
      width: 680rpx;
    }
    .likelist {
      margin-top: 20px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      .like {
        width: 45px;
        height: 45px;
        background-color: #cfd8e2;
        border-radius: 50%;
        .iconfont {
          font-size: 25px;
          text-align: center;
          line-height: 45px;
          color: #fff;
        }
      }
      text {
        display: block;
        padding: 10px 0;
        text-align: center;
        font-size: 12px;
        color: #c6c6c6;
      }
      .head-img {
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;
        image {
          width: 36px;
          height: 36px;
          border-radius: 50%;
          margin-right: 6px;
        }
        .last-head {
          display: inline-block;
          color: #fff;
          width: 36px;
          height: 36px;
          font-size: 12px;
          line-height: 36px;
          text-align: center;
          border-radius: 50%;
          background-image: linear-gradient(45deg, #b5c1d2, #e7effb);
        }
      }
    }
    .you-like {
      text {
        display: block;
        margin: 15px 0;
        color: #0f2540;
        font-size: 14px;
      }
    }
    .perhaps_like {
      display: flex;
      flex-direction: row;
      align-items: center;
      margin: 10px 0;
      .left {
        image {
          width: 94px;
          height: 94px;
          border-radius: 5px;
        }
        margin-right: 20px;
      }

      .right {
        margin-left: 20px;
        width: 400rpx;
        height: 80rpx;
        .like-title {
          display: inline-block;
          font-size: 16px;
          margin-bottom: 10px;
          color: #0f2540;
          line-height: 20px;
        }
        .like-username {
          display: inline-block;
          margin-top: 10px;
          color: #c6c6c6;
          font-size: 12px;
          line-height: 12px;
        }
      }
    }
  }
}
</style>
