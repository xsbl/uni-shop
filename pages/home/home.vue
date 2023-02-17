<template>
	<view>
		sisheng home
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

</style>
