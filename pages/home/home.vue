<template>
	<view>
		<view class="headBox">
			<view class="locationBox">
				<view>
					<image src="../../static/home/location.png" class="Icon"></image>
					<text>金沙路越秀滨海新城</text>
				</view>
				<view>
					<image src="../../static/home/ScanCode.png" class="Icon"></image>
					<image src="../../static/home/message.png" class="Icon"></image>
				</view>
			</view>
		</view>
	<view class="contentBox">
		
	</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			}
		},
		methods: {

		}
	}
</script>

<style scoped lang="less">
	@import url("../../static/common/uni.less");
	.headBox {
		padding-top: 100rpx;
		width: 100%;
		height: 180rpx;
		background-color: @themeColor;
		color: white;
		
		.locationBox {
			display: flex;
			justify-content: space-between;
			padding: 0 20rpx;

			.Icon {
				width: 40rpx;
				height: 40rpx;
			}
			.Icon:nth-child(2){
				margin-left:40rpx
			}
		}
	}
	.contentBox{
		background-color: white;
		width: 100%;
		height: 1000rpx;
		margin-top: -100rpx;
		border-radius: 34rpx;
	}
</style>
