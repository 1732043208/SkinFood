<template>
	<view style="position: relative;" @touchstart="touchStart" @touchend="touchEnd">
		<view class="cart" :class="{'isCartShow':!isSlide}" v-if="!isSlide" @click="pushCart">
			<image src="../../static/home/cart.png" mode="widthFix" style="width: 70%;height: 70%;vertical-align: middle;"></image>
		</view>
		<!-- 微信小程序运行代码 -->
		<!-- #ifdef MP-WEIXIN -->
		<view class="headBox" v-if="!isChange">

			<view class="locationBox">
				<view class="title">
					<text>皮了么</text>
					<text>|</text>
				</view>
				<view class="usersLocationBox" v-if="isGetLocation">
					<view>
						<image src="../../static/home/headBox/location.png" class="SmallIcon"></image>
					</view>
					<view class="usersLocationName">{{addressName}}</view>
					<view>
						<image src="../../static/home/headBox/down.png" class="headDownImg"></image>
					</view>
				</view>
				<view v-if="!isGetLocation" style="font-size: 26rpx;">
					暂无获取到位置信息
				</view>
			</view>
			<view class="searchBox">
				<input type="text" placeholder="糕大上蛋糕店 100减3" class="searchInput"></input>
				<image src="../../static/home/headBox/search.png" class="SmallIcon"></image>
			</view>
		</view>
		<view class="headBoxSecond" v-if="isChange">
			<view class="headBoxFixed">
				<view class="searchBoxSecond">
					<input type="text" placeholder="糕大上蛋糕店 100减3" class="searchInputSecond"></input>
					<image src="../../static/home/headBox/search.png" class="SmallIcon"></image>
				</view>
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
		<view class="recommendBox">
			<view class="suggestBox" :class="{'is_fixed':isfixed}">
				<h1 class="title">附近推荐</h1>
				<view class="recommendTitles">
					<block v-for="(item,index) in recommendTitles">
						<view class="recommendItem" @click="suggestClick(index)" :class="{'suggestChange':currentIndex===index}">{{item}}</view>
					</block>
				</view>
			</view>
			<view class="recommendDetails" :class="{'is_fixedSecond':isfixed}">
				<view v-for="(item,index) in recommendDetailsList" :key="item.id">

					<view class="shopDetails">

						<view class="left">
							<image :src="item.src"></image>
						</view>
						<view class="right">
							<view class="rightTitleBox">
								<h1>{{item.title}}</h1>
								<image src="../../static/home/recommends/ellipsis-v.png" class="ellipsis"></image>
							</view>
							<view class="rightFirstBox">
								<view class="rightFirstBoxLeft">
									<text>{{item.score}}分</text>
									<text>月售{{item.sales}}</text>
								</view>
								<view class="rightFirstBoxRight">
									<text>{{item.time}}分钟</text>
									<text>{{item.distance}}</text>
								</view>
							</view>
							<view class="rightSecondBox">

								<text>起送￥{{item.Send}}</text>
								<view v-if="item.ShippingPrice!=='0'">
									<text>配送￥{{item.ShippingPrice}}</text>
									<text class="oldPrice">￥{{item.oldShippingPrice}}</text>
								</view>
								<view v-if="item.ShippingPrice==='0'">
									<text>免配送费</text>
									<text class="oldPrice">￥{{item.oldShippingPrice}}</text>
								</view>
							</view>
							<view class="rightThirdBox" v-if="item.isDetection">
								<view>
									<text>已检测体温，请放心食用</text>
								</view>
							</view>
							<view class="rightFourth">
								<view v-for="value in item.discountList">
									<view class="cutBox">{{value}}</view>
								</view>
							</view>
						</view>
					</view>

				</view>
			</view>
		</view>
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
				<image src="../../static/home/headBox/ScanCode.png" class="scanCode"></image>
				<image src="../../static/home/headBox/message.png" class="message"></image>
			</view>
		</view>
	</view>
	<view class="contentBox">
		<view class="searchBox">
			<view class="left">
				<image src="../../static/home/headBox/search.png" class="searchIcon"></image>
				<input type="text" placeholder="汉堡王 55减20">
			</view>
			<view class="search">搜索</view>
		</view>
		<swiper class="swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration"
		 :circular="true">
			<swiper-item>
				<image src="../../static/home/swiper.png" mode="widthFix" class="swiper-item"></image>
			</swiper-item>
			<swiper-item>
				<image src="../../static/home/swiper.png" mode="widthFix" class="swiper-item"></image>
			</swiper-item>
			<swiper-item>
				<image src="../../static/home/swiper.png" mode="widthFix" class="swiper-item"></image>
			</swiper-item>
		</swiper>
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
		<view class="recommendBox">
			<view class="suggestBox" :class="{'is_fixed':isfixed}">
				<h1 class="title">附近推荐</h1>
				<view class="recommendTitles">
					<block v-for="(item,index) in recommendTitles">
						<view class="recommendItem" @click="suggestClick(index)" :class="{'suggestChange':currentIndex===index}">{{item}}</view>
					</block>
				</view>
			</view>
			<view class="recommendDetails" :class="{'is_fixedSecond':isfixed}">
				<view v-for="(item,index) in recommendDetailsList" :key="item.id">

					<view class="shopDetails">

						<view class="left">
							<image :src="item.src"></image>
						</view>
						<view class="right">
							<view class="rightTitleBox">
								<h1>{{item.title}}</h1>
								<image src="../../static/home/recommends/ellipsis-v.png" class="ellipsis"></image>
							</view>
							<view class="rightFirstBox">
								<view class="rightFirstBoxLeft">
									<text>{{item.score}}分</text>
									<text>月售{{item.sales}}</text>
								</view>
								<view class="rightFirstBoxRight">
									<text>{{item.time}}分钟</text>
									<text>{{item.distance}}</text>
								</view>
							</view>
							<view class="rightSecondBox">

								<text>起送￥{{item.Send}}</text>
								<view v-if="item.ShippingPrice!=='0'">
									<text>配送￥{{item.ShippingPrice}}</text>
									<text class="oldPrice">￥{{item.oldShippingPrice}}</text>
								</view>
								<view v-if="item.ShippingPrice==='0'">
									<text>免配送费</text>
									<text class="oldPrice">￥{{item.oldShippingPrice}}</text>
								</view>
							</view>
							<view class="rightThirdBox" v-if="item.isDetection">
								<view>
									<text>已检测体温，请放心食用</text>
								</view>
							</view>
							<view class="rightFourth">
								<view v-for="value in item.discountList">
									<view class="cutBox">{{value}}</view>
								</view>
							</view>
						</view>
					</view>

				</view>
			</view>
		</view>
	</view>
	<!-- #endif -->

	</view>
</template>

<script>
	import json from '../../static/common/network.json'
	import amap from '../../common/amap-wx.130.js'
	export default {
		data() {
			return {
				navImgList: [],
				navIconList: [],
				recommendTitles: [],
				recommendDetailsList: [],
				//页面滚动的距离
				rect: '',
				//组件距离顶部的距离
				menutop: '',
				//"附近推荐"是否吸顶
				isfixed: false,
				//顶部搜索框状态
				isChange: false,
				amapPlugin: null,
				//高德key
				key: '869978775d6b751ea6cc8f6283cb363c',
				//用户当前位置
				addressName: '',
				currentIndex: 0,
				isGetLocation: false,
				// 开始与结束标识
				isSlide: false,
				// 监听手指是否触摸着屏幕没放开
				isTouch: false,
				indicatorDots: true,
				autoplay: true,
				interval: 2000,
				duration: 500
			}
		},
		onLoad() {

			// 获取json数据
			this.getData()
			// #ifdef MP-WEIXIN
			this.amapPlugin = new amap.AMapWX({
				key: this.key
			});
			//获取当前位置(小程序)
			this.getRegeo();

			// #endif

		},
		onReady() {
			// 监听筛选组件距离顶部的距离
			const query = uni.createSelectorQuery()
			query.select('.suggestBox').boundingClientRect((res) => {
				// console.log(res.height)
			})
			query.exec((res) => {
				this.menutop = res[0].top;
				console.log('asdasdas' + this.menutop)
			})
		},

		methods: {
			touchStart() {
				this.isTouch = true
			},
			touchEnd() {
				this.isTouch = false
				this.isSlide = false
			},
			// #ifdef MP-WEIXIN
			getRegeo() {
				uni.showLoading({
					title: '获取信息中'
				});
				this.amapPlugin.getRegeo({
					success: (data) => {
						console.log(data)
						this.addressName = data[0].name;
						this.isGetLocation = true
						uni.hideLoading();

					}
				});
			},

			isLikeFunc(index) {
				console.log(index)
				this.isLike = index
			},


			// #endif
			suggestClick(index) {
				this.currentIndex = index
			},
			getData() {
				// json假数据模拟网络请求
				this.navImgList = json.result.data["0"].navImgList;
				this.navIconList = json.result.data["0"].navIconList;
				this.recommendTitles = json.result.data["0"].recommendTitles;
				this.recommendDetailsList = json.result.data["0"].recommendDetailsList;

			},
			pushCart() {
				uni.switchTab({
					url: '../order/order'
				});
			}
		},
		computed: {
			// #ifdef MP-WEIXIN
			// 监听顶部搜索框状态变化
			isChangeFunc() {
				if (this.rect >= 10) {
					this.isChange = true
				} else {
					this.isChange = false
				}
			},

			// #endif

		},
		onPageScroll(e) {
			// console.log(e.scrollTop)
			//获取当前高度与顶部的距离
			this.rect = e.scrollTop;
			// console.log('我是rect----------' + this.rect)

			// 75是吸顶盒子的高度
			if (this.rect > (this.menutop - 75)) {
				this.isfixed = true
			} else {
				this.isfixed = false
			}

			//判断滑动是否已经结束
			clearTimeout(time)
			this.isSlide = true
			let time = setTimeout(() => {
				console.log('结束滚动')
				if (!this.isTouch) {
					this.isSlide = false
				}

			}, 100)

		}
	}
</script>

<style scoped lang="less">
	@import url("../../static/common/uni.less");

	@keyframes move {

		/*定义关键帧*/
		0% {
			right: -100rpx;
		}

		100% {
			right: 16rpx;
		}
	}

	.isCartShow {
		animation-name: move;
		animation-duration: 1s;
	}


	.cart {
		width: 100rpx;
		height: 100rpx;
		border-radius: 100rpx;
		position: fixed;
		bottom: 30rpx;
		right: 16rpx;
		background-color: white;
		text-align: center;
		line-height: 100rpx;
		box-shadow: 0px 4px 20px 0px rgba(8, 8, 8, 0.1);
	}

	// 微信小程序执行的代码
	/* #ifdef MP-WEIXIN */


	.is_fixed {
		position: fixed;
		left: 0;
		top: 144rpx;
		right: 0;
	}

	.is_fixedSecond {
		margin-top: 146rpx;
	}

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

			.usersLocationBox {
				font-size: 26rpx;

				display: flex;

				.usersLocationName {
					width: 320rpx;
					white-space: nowrap;
					overflow: hidden;
					text-overflow: ellipsis;
				}

				.headDownImg {
					width: 18rpx;
					height: 18rpx;
					margin-bottom: -4rpx;
				}
			}
		}
	}

	.searchBox {
		position: relative;
		background-color: white;
		width: 94%;
		height: 70rpx;
		margin: 24rpx auto;
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

	.headBoxSecond {
		padding-top: 60rpx;
		width: 100%;
		height: 260rpx;
		background-color: @themeColor;

		.headBoxFixed {
			padding-top: 56rpx;
			width: 100%;
			height: 90rpx;
			background-color: @themeColor;
			position: fixed;
			top: 0rpx;


			.searchBoxSecond {
				margin-left: 20rpx;
				background-color: white;
				width: 66%;
				height: 60rpx;
				border-radius: 60rpx;
				line-height: 60rpx;
				position: relative;
				margin-top: 4rpx;

				.SmallIcon {
					position: absolute;
					top: 50%;
					transform: translateY(-50%);
					margin-left: 20rpx;
				}

				.searchInputSecond {
					color: black;
					height: 100%;
					padding-left: 80rpx;
					font-size: 26rpx;
				}
			}

		}
	}



	.contentBox {
		background-image: linear-gradient(#ffffff, #ffffff, #f5f5f5);
		width: 100%;
		padding-bottom: 60rpx;
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

	.recommendBox {
		width: 100%;
		margin-top: -40rpx;
		background-color: white;
		border-radius: 30rpx;

		.suggestBox {
			background-color: white;

			.title {
				padding-top: 20rpx;
				margin-left: 24rpx;
				margin-bottom: 8rpx;
				font-weight: 700;
			}

			.recommendTitles {
				display: flex;
				text-align: center;
				font-size: 24rpx;
				margin-bottom: 10rpx;

				.recommendItem {
					flex: 1;
					border-radius: 16rpx;
					margin: 10rpx 14rpx;
					padding: 14rpx 10rpx;
					background-color: #F3F3F3;
				}

				.suggestChange {
					color: #1997DE;
					background-color: #CCEDFF;
				}
			}
		}


		.shopDetails {
			display: flex;
			box-sizing: content-box;
			padding: 10rpx 20rpx;

			.left {
				margin-right: 20rpx;

				image {
					width: 160rpx;
					height: 160rpx;
				}
			}

			.right {
				width: 76%;

				.rightTitleBox {
					display: flex;
					justify-content: space-between;

					.ellipsis {
						margin-top: 10rpx;
						width: 24rpx;
						height: 24rpx;
					}
				}


				.rightFirstBox {
					display: flex;
					justify-content: space-between;
					font-size: 24rpx;
					margin-top: 8rpx;
					color: #575757;

					.rightFirstBoxLeft {
						text:first-child {
							margin-right: 20rpx;
							color: #E36515;
						}
					}

					.rightFirstBoxRight {
						text:first-child {
							margin-right: 20rpx;
						}
					}
				}

				.rightSecondBox {
					display: flex;
					font-size: 24rpx;
					color: #575757;
					margin-top: 8rpx;

					view {

						text:first-child {
							margin-left: 20rpx;
						}

						.oldPrice {
							color: #B1B1B1;
							font-size: 22rpx;
							text-decoration: line-through;
							margin-left: 4rpx;
						}
					}

				}

				.rightThirdBox {
					margin-top: 6rpx;
					width: 250rpx;
					background-color: #FFEEE2;
					font-size: 22rpx;
					color: #D1651F;
					border-radius: 6rpx;
					text-align: center;
					padding: 4rpx 0rpx;
				}

				.rightFourth {
					height: 26rpx;
					overflow: hidden;
					padding-bottom: 40rpx;
					border-bottom: 1px solid #F6F6F6;
					display: flex;
					flex-wrap: wrap;

					font-size: 22rpx;
					color: #DE6050;

					.cutBox {
						border-radius: 8rpx;
						padding: 2rpx 6rpx;
						margin-right: 10rpx;
						margin-top: 10rpx;
						border: 1px solid #F7C7C1;
					}
				}

				h1 {
					font-size: 30rpx;
					font-weight: 700;
				}
			}
		}
	}

	/* #endif */

	// 除微信小程序外执行的代码
	/* #ifndef MP-WEIXIN */
	.headBox {
		padding-top: 80rpx;
		width: 100%;
		height: 180rpx;
		background-color: @themeColor;
		color: white;

		.locationBox {
			display: flex;
			justify-content: space-between;
			padding: 0 20rpx;
			height: 80rpx;
			line-height: 80rpx;

			.scanCode {
				width: 66rpx;
				height: 66rpx;
			}

			.message {
				width: 60rpx;
				height: 60rpx;
				margin-left: 20rpx;
			}
		}
	}

	.contentBox {
		background-color: white;
		width: 100%;
		height: 1000rpx;
		margin-top: -100rpx;
		border-radius: 38rpx;
		padding-top: 20rpx;
		font-size: 24rpx;

		.swiper {
			width: 94%;
			height: 200rpx;
			margin: 20rpx auto;
			margin-bottom: 0;

			.swiper-item {
				width: 100%;
			}
		}

		.searchBox {
			display: flex;
			justify-content: space-between;
			width: 94%;
			height: 70rpx;
			line-height: 70rpx;
			background-color: #F2F3F5;
			margin: 0 auto;
			border-radius: 70rpx;


			.left {
				display: flex;
				margin-left: 20rpx;

				input {
					margin-left: 20rpx;
					font-size: 26rpx;
					height: 70rpx;
				}

				.searchIcon {
					width: 38rpx;
					height: 38rpx;
					margin-top: 18rpx;
				}
			}

			.search {
				color: white;
				background-color: @themeColor;
				border-radius: 70rpx;
				width: 120rpx;
				margin: 6rpx;
				line-height: 58rpx;
				text-align: center;
				font-size: 30rpx;
			}
		}

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

		.recommendBox {
			width: 100%;
			margin-top: 20rpx;
			background-color: white;
			border-radius: 30rpx;

			.suggestBox {
				background-color: white;

				.title {
					padding-top: 20rpx;
					margin-left: 24rpx;
					margin-bottom: 8rpx;
					font-weight: 700;
					font-size: 34rpx;
				}

				.recommendTitles {
					display: flex;
					text-align: center;
					font-size: 24rpx;
					margin-bottom: 10rpx;

					.recommendItem {
						flex: 1;
						border-radius: 16rpx;
						margin: 10rpx 14rpx;
						padding: 14rpx 10rpx;
						background-color: #F3F3F3;
					}

					.suggestChange {
						color: #1997DE;
						background-color: #CCEDFF;
					}
				}
			}


			.shopDetails {
				display: flex;
				box-sizing: content-box;
				padding: 10rpx 20rpx;

				.left {
					margin-right: 20rpx;

					image {
						width: 160rpx;
						height: 160rpx;
					}
				}

				.right {
					width: 76%;

					.rightTitleBox {
						display: flex;
						justify-content: space-between;

						.ellipsis {
							margin-top: 10rpx;
							width: 24rpx;
							height: 24rpx;
						}
					}


					.rightFirstBox {
						display: flex;
						justify-content: space-between;
						font-size: 24rpx;
						margin-top: 8rpx;
						color: #575757;

						.rightFirstBoxLeft {
							text:first-child {
								margin-right: 20rpx;
								color: #E36515;
							}
						}

						.rightFirstBoxRight {
							text:first-child {
								margin-right: 20rpx;
							}
						}
					}

					.rightSecondBox {
						display: flex;
						font-size: 24rpx;
						color: #575757;
						margin-top: 8rpx;

						view {

							text:first-child {
								margin-left: 20rpx;
							}

							.oldPrice {
								color: #B1B1B1;
								font-size: 22rpx;
								text-decoration: line-through;
								margin-left: 4rpx;
							}
						}

					}

					.rightThirdBox {
						margin-top: 6rpx;
						width: 270rpx;
						background-color: #FFEEE2;
						font-size: 22rpx;
						color: #D1651F;
						border-radius: 6rpx;
						text-align: center;
						padding: 4rpx;

					}

					.rightFourth {
						height: 26rpx;
						overflow: hidden;
						padding-bottom: 40rpx;
						border-bottom: 1px solid #F6F6F6;
						display: flex;
						flex-wrap: wrap;

						font-size: 22rpx;
						color: #DE6050;

						.cutBox {
							border-radius: 8rpx;
							padding: 2rpx 6rpx;
							margin-right: 10rpx;
							margin-top: 10rpx;
							border: 1px solid #F7C7C1;
						}
					}

					h1 {
						font-size: 30rpx;
						font-weight: 700;
					}
				}
			}
		}
	}

	/* #endif */
</style>
