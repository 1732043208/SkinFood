<template>
	<view>
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
	</view>
	<!-- #endif -->

	</view>
</template>

<script>
	import amap from '../../common/amap-wx.130.js'
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
				}],
				recommendTitles: ['津贴优惠', '满减优惠', '下单返红包', '进店领红包'],
				recommendDetailsList: [{
						title: '富鸽一家',
						score: '4.7',
						sales: '43',
						time: '30',
						distance: '136m',
						src: '../../static/home/recommends/recommendImg1.png',
						Send: '20',
						ShippingPrice: '0.7',
						oldShippingPrice: '4',
						isDetection: true,
						discountList: ['11减10', '30减20', '88减28', '128减36']
					},
					{
						title: '花氧均衡营养美食(南沙店)',
						score: '4.0',
						sales: '138',
						time: '30',
						distance: '2.2km',
						src: '../../static/home/recommends/recommendImg2.png',
						Send: '20',
						ShippingPrice: '0',
						oldShippingPrice: '4',
						isDetection: false,
						discountList: ['10减6', '100减8', '200减16', '400减35', '500减40']
					},
					{
						title: '鱼别走·酸菜鱼(南沙店)',
						score: '4.6',
						sales: '1518',
						time: '30',
						distance: '3.1km',
						src: '../../static/home/recommends/recommendImg3.png',
						Send: '0',
						ShippingPrice: '0',
						oldShippingPrice: '5',
						isDetection: false,
						discountList: ['20减19', '52减23', '80减36', '110减46', '0.1元特价']
					},
					{
						title: '木桶饭(金洲店)',
						score: '4.4',
						sales: '258',
						time: '36',
						distance: '2.7km',
						src: '../../static/home/recommends/recommendImg4.png',
						Send: '20',
						ShippingPrice: '0',
						oldShippingPrice: '3',
						isDetection: true,
						discountList: ['36减5', '50减6', '2元店铺红包']
					},
					{
						title: '港堡汉堡·炸鸡(金洲店)',
						score: '4.7',
						sales: '2459',
						time: '38',
						distance: '3.1km',
						src: '../../static/home/recommends/recommendImg5.png',
						Send: '20',
						ShippingPrice: '0.9',
						oldShippingPrice: '4',
						isDetection: false,
						discountList: ['35减19', '46减27', '66减34', '85减39']
					},
					{
						title: '吃湘喝辣快餐',
						score: '4.5',
						sales: '364',
						time: '30',
						distance: '2.4km',
						src: '../../static/home/recommends/recommendImg6.png',
						Send: '15',
						ShippingPrice: '0',
						oldShippingPrice: '3',
						isDetection: true,
						discountList: ['30减8', '50减10', '2元店铺红包']
					},
					{
						title: '排骨米饭',
						score: '4.1',
						sales: '913',
						time: '30',
						distance: '2.5km',
						src: '../../static/home/recommends/recommendImg7.png',
						Send: '15',
						ShippingPrice: '0',
						oldShippingPrice: '3',
						isDetection: false,
						discountList: ['25减8', '38减12', '80减23', '100减26']
					},

				],
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

			}
		},
		onLoad() {
			// #ifdef MP-WEIXIN
			// 监听筛选组件距离顶部的距离
			const query = uni.createSelectorQuery()
			query.select('.suggestBox').boundingClientRect((res) => {
				// console.log(res.height)
			})
			query.exec((res) => {
				this.menutop = res[0].top;
			})

			this.amapPlugin = new amap.AMapWX({
				key: this.key
			});
			//获取当前位置(小程序)
			this.getRegeo();
			// #endif

		},

		methods: {
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
			suggestClick(index) {
				this.currentIndex = index
			},
			isLikeFunc(index) {
				console.log(index)
				this.isLike = index
			}
			// #endif

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
			//监听“附近推荐”是否吸顶
			isFixedFunc() {
				// 75是吸顶盒子的高度
				if (this.rect > (this.menutop - 75)) {
					this.isfixed = true
				} else {
					this.isfixed = false
				}
			}
			// #endif

		},
		onPageScroll(e) {
			// console.log(e.scrollTop)
			//获取当前高度与顶部的距离
			this.rect = e.scrollTop;
			console.log(this.rect)
		}
	}
</script>

<style scoped lang="less">
	@import url("../../static/common/uni.less");

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
			}
		}
	}

	/* #endif */
</style>
