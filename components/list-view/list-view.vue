<template>
	<view class="fatherBox">
		<view class="leftBox">
			<!-- 左边部分填充的内容 -->
			<slot name="left"></slot>
		</view>
		<view class="rightBox">
			<!-- 右边部分填充的内容 -->
			<slot name="right"></slot>
			<image src="../../static/mine/right.png" mode="widthFix" class="Icon"></image>
		</view>
	</view>
</template>

<script>
	export default {

		data() {
			return {

			}
		},

		onLoad() {

		},
		methods: {

		}
	}
</script>

<style scoped lang="less">
	.fatherBox {
		display: flex;
		height: 110rpx;
		line-height: 110rpx;

		.leftBox {
			text-align: center;
			flex: 1;
		}

		.rightBox {
			flex: 4;
			display: flex;
			justify-content: space-between;
			border-bottom: 1rpx solid #EBEBEB;
			font-size: 34rpx;
			.Icon{
				margin-top: 55rpx;
				margin-right: 20rpx;
				width: 30rpx;
				transform: translateY(-50%);
			}
		}
	}
</style>
