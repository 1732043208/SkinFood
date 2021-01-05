<template>
	<view>
		<!-- 微信小程序运行代码 -->
		<!-- #ifdef MP-WEIXIN -->
		<view class="headBox">
			<view class="locationBox">
				<view class="title">
					<text>皮了么</text>
					<text>|</text>
				</view>
				<view>
					<image src="../../static/home/location.png" class="Icon"></image>
					金沙路越秀滨海新城
				</view>
			</view>
			<view class="searchBox">
				<input type="text" placeholder="糕大上蛋糕店 100减3" class="searchInput"></input>
				<image src="../../static/home/headBox/search.png" class="Icon"></image>
			</view>
		</view>
		<view class="contentBox">

		</view>
		<!-- #endif -->
		<!-- 除了微信小程序之外运行的代码 -->
		<!-- #ifndef MP-WEIXIN -->
		<view class="headBox">
			<view class="locationBox">
				<view>
					<image src="../../static/home/headBox/location.png" class="Icon"></image>
					<text>金沙路越秀滨海新城</text>
				</view>
				<view>
					<image src="../../static/home/headBox/ScanCode.png" class="Icon"></image>
					<image src="../../static/home/headBox/message.png" class="Icon"></image>
				</view>
			</view>
		</view>
		<view class="contentBox">

		</view>
		<!-- #endif -->

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

	// 微信小程序执行的代码
	/* #ifdef MP-WEIXIN */
	.headBox {
		padding-top: 60rpx;
		width: 100%;
		height: 260rpx;
		background-color: @themeColor;
		color: white;

		.locationBox {
			display: flex;
			padding: 0 20rpx;
			height: 50rpx;
			line-height: 50rpx;

			.title {
				margin-right: 14rpx;
			}

			.title>text:first-child {
				margin-right: 14rpx;
				font-weight: 700;
				font-size: 34rpx;
			}
		}
	}

	.searchBox {
		position: relative;
		background-color: white;
		width: 94%;
		height: 70rpx;
		margin: 20rpx auto;
		border-radius: 70rpx;
		line-height: 70rpx;

		.Icon {
			position: absolute;
			top: 16rpx;
			margin-left: 20rpx;
		}

		.searchInput {
			color: black;
			height: 100%;
			padding-left: 80rpx;
			font-size: 26rpx;
		}
	}

	.contentBox {
		background-color: white;
		width: 100%;
		height: 1000rpx;
		margin-top: -100rpx;
		border-radius: 34rpx;
	}

	/* #endif */

	// 除微信小程序外执行的代码
	/* #ifndef MP-WEIXIN */
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



			.Icon:nth-child(2) {
				margin-left: 40rpx
			}

		}
	}

	.contentBox {
		background-color: white;
		width: 100%;
		height: 1000rpx;
		margin-top: -100rpx;
		border-radius: 34rpx;
	}

	/* #endif */
</style>
