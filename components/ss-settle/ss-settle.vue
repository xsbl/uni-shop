<template>
  <!-- 最外层的容器 -->
  <!-- 最外层的容器 -->
  <view class="my-settle-container">
    <!-- 全选区域 -->
    <label class="radio" @click="changeAllState">
      <radio color="#C00000" :checked="isFullCheck" /><text>全选</text>
    </label>
  
    <!-- 合计区域 -->
    <view class="amount-box">
      合计:<text class="amount">￥{{checkedGoodsAmount}}</text>
    </view>
  
    <!-- 结算按钮 -->
    <view class="btn-settle">结算({{checkedCount}})</view>
  </view>
</template>

<script>
	import { mapGetters, mapMutations  } from 'vuex'
	
export default {
  data() {
    return {}
  },
  computed: {
      ...mapGetters('m_cart', ['checkedCount', 'total', 'checkedGoodsAmount']),
	  // 2. 是否全选
	      isFullCheck() {
	        return this.total === this.checkedCount
	      },
    },
	methods: {
	    ...mapMutations('m_cart', ['updateAllGoodsState']),
		changeAllState() {
		    // 修改购物车中所有商品的选中状态
		    // !this.isFullCheck 表示：当前全选按钮的状态取反之后，就是最新的勾选状态
		    this.updateAllGoodsState(!this.isFullCheck)
		  }
	  },
}
</script>

<style lang="scss">
.my-settle-container {
  /* 底部固定定位 */
  position: fixed;
  bottom: 0;
  left: 0;
  /* 设置宽高和背景色 */
  width: 100%;
  height: 50px;
  
  // 将背景色从 cyan 改为 white
    background-color: white;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-left: 5px;
    font-size: 14px;
  
    .radio {
      display: flex;
      align-items: center;
    }
  
    .amount {
      color: #c00000;
	  font-weight: bold;
    }
  
    .btn-settle {
      height: 50px;
      min-width: 100px;
      background-color: #c00000;
      color: white;
      line-height: 50px;
      text-align: center;
      padding: 0 10px;
    }
}
</style>