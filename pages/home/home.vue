<template>
	<view>
		<!-- 轮播图的区域 -->
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" :circular="true">
		  <swiper-item v-for="(item, i) in swiperList" :key="i">
			<navigator class="swiper-item" :url="'/subpkg/goods_detail/goods_detail?goods_id=' + item.goods_id">
			  <image :src="item.image_src"></image>
			</navigator>
		  </swiper-item>
		</swiper>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// 这是轮播图的数据列表
				swiperList: [],
			};
		},
		onLoad() {
			console.log('hhhhhhhhhh')
		      // 调用方法，获取轮播图的数据
		      this.getSwiperList()
		},
		methods: {
		  async getSwiperList() {
			const { data: res } = await uni.$http.get('/api/public/v1/home/swiperdata')
			// 请求失败
			if (res.meta.status !== 200) {
				return uni.showToast({
				  title: '数据请求失败！',
				  duration: 1500,
				  icon: 'none',
				})
			}
			this.swiperList = res.message
		  },
		}
	}
</script>

<style lang="scss">
  swiper {
    height: 330rpx;

    .swiper-item,
    image {
      width: 100%;
      height: 100%;
    }
  }

  .nav-list {
    display: flex;
    justify-content: space-around;
    margin: 15px 0;

    .nav-img {
      width: 128rpx;
      height: 140rpx;
    }
  }

  .floor-title {
    width: 100%;
    height: 60rpx;
  }

  .right-img-box {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
  }

  .floor-img-box {
    display: flex;
    padding-left: 10rpx;
  }
</style>
