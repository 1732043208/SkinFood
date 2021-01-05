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
					<image src="../../static/home/headBox/location.png" class="SmallIcon"></image>
					金沙路越秀滨海新城
				</view>
			</view>
			<view class="searchBox">
				<input type="text" placeholder="糕大上蛋糕店 100减3" class="searchInput"></input>
				<image src="../../static/home/headBox/search.png" class="SmallIcon"></image>
			</view>
		</view>
		<view class="contentBox">
			<view class="navImg">
				<view class="navImgBox" v-for="item in navImgList" :key="item.id">
					<image :src="item.src" class="BigIcon"></image>
					<view>{{item.title}}</view>
				</view>
			</view>
			<view class="navIcon">
				<view class="navIconBox" v-for="item in navIconList" :key="item.id">
					<image :src="item.src" class="MiddleIcon"></image>
					<view>{{item.title}}</view>
				</view>
			</view>
			<image src="../../static/home/navBar/advertising.png" class="advertising"></image>
		</view>
		<!-- #endif -->
		<!-- 除了微信小程序之外运行的代码 -->
		<!-- #ifndef MP-WEIXIN -->
		<view class="headBox">
			<view class="locationBox">
				<view>
					<image src="../../static/home/headBox/location.png" class="SmallIcon"></image>
					<text>金沙路越秀滨海新城</text>
				</view>
				<view>
					<image src="../../static/home/headBox/ScanCode.png" class="SmallIcon"></image>
					<image src="../../static/home/headBox/message.png" class="SmallIcon"></image>
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
				navImgList: [{
					id: 1,
					title: '美食',
					src: '../../static/home/navBar/navImg1.png'
				}, {
					id: 2,
					title: '超市便利',
					src: '../../static/home/navBar/navImg2.png'
				}, {
					id: 3,
					title: '水果',
					src: '../../static/home/navBar/navImg3.png'
				}, {
					id: 4,
					title: '送药上门',
					src: '../../static/home/navBar/navImg4.png'
				}, {
					id: 5,
					title: '甜品饮品',
					src: '../../static/home/navBar/navImg5.png'
				}],
				navIconList: [{
					id: 1,
					title: '分享赚钱',
					src: '../../static/home/navBar/navIcon1.png'
				}, {
					id: 2,
					title: '买菜',
					src: '../../static/home/navBar/navIcon2.png'
				}, {
					id: 3,
					title: '配送减免',
					src: '../../static/home/navBar/navIcon3.png'
				}, {
					id: 4,
					title: '订了么',
					src: '../../static/home/navBar/navIcon4.png'
				}, {
					id: 5,
					title: '地方美食',
					src: '../../static/home/navBar/navIcon5.png'
				}]
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

		.SmallIcon {
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
		background-image: linear-gradient(#ffffff, #f5f5f5);
		width: 100%;
		margin-top: -100rpx;
		border-radius: 34rpx;
		font-size: 24rpx;

		.navImg {
			display: flex;

			.navImgBox {
				flex: 1;
				text-align: center;
				margin-top: 30rpx;

				}
		}

		.navIcon {
			margin-top: 24rpx;
			display: flex;

			.navIconBox {
				flex: 1;
				text-align: center;
			}
		}

		.advertising {
			width: 94%;
			height: 180rpx;
			margin-top: 20rpx;
			margin-left: 3%;
		}
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

			.SmallIcon:nth-child(2) {
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
