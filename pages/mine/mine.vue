<template>
	<view>
		<view class="navBox"></view>
		<view class="headBox">
			<view class="leftBox">
				<open-data type="userNickName" class="UserName"></open-data>
				<view>再忙，也要记得吃饭哟~</view>
			</view>
			<view class="rightBox">
				<button open-type="getUserInfo"></button>
				<open-data type="userAvatarUrl"></open-data>
			</view>
		</view>
		<view class="contentBox">
			<view class="firstBox">
				<view class="leftBox">
					<view class="firstLine">
						<text>红包</text>
						<image src="../../static/mine/redPacket.png" mode="widthFix" class="icons"></image>
					</view>
					<view class="secondLine">
						<text>6</text>
						<text>个未使用</text>
					</view>
				</view>
				<view class="rightBox">
					<view class="firstLine">
						<text>余额</text>
						<image src="../../static/mine/letter.png" mode="widthFix" class="icons"></image>
					</view>
					<view class="secondLine">
						<text>￥2</text>
					</view>
				</view>
			</view>
			<view class="secondBox">
				<view class="leftBox">
					<view>点餐提醒</view>
					<view style="color: #929292;font-size: 26rpx;">已有
						<text style="display: inline-block;margin: 0 10rpx;">93331</text>人提醒自己按时吃饭</view>
				</view>
				<view class="rightBox">
					<text>立即开启</text>
				</view>
			</view>
			<view v-for="item in listViews" :key="item.id">
				<list-view>
					<template #left>
						<image :src="item.src" mode="widthFix" class="listViewIcon"></image>
					</template>
					<template #right>
						<text>{{item.title}}</text>
					</template>
				</list-view>
			</view>
		</view>
	</view>
</template>

<script>
	import ListView from '../../components/list-view/list-view.vue'
	export default {
		data() {
			return {
				listViews: [{
					id: 1,
					src: '../../static/mine/address.png',
					title: '我的地址'
				}, {
					id: 2,
					src: '../../static/mine/collection.png',
					title: '我的收藏'
				}, {
					id: 3,
					src: '../../static/mine/gift.png',
					title: '推荐有奖'
				}, {
					id: 4,
					src: '../../static/mine/service.png',
					title: '我的客服'
				}, {
					id: 5,
					src: '../../static/mine/rules.png',
					title: '规则中心'
				}, ]
			}
		},
		components: {
			ListView
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style scoped lang="less">
	.navBox {
		height: 129rpx;
		background-color: #fff;
		line-height: 150rpx;
		color: black;
		padding-left: 30rpx;
	}


	.headBox {
		display: flex;
		justify-content: space-between;
		margin: 10rpx 30rpx 10rpx 30rpx;

		.leftBox {
			color: #929292;
			font-size: 28rpx;

			.UserName {
				font-size: 50rpx;

				color: black;
			}
		}

		.rightBox {
			width: 140rpx;
			height: 140rpx;
			overflow: hidden;
			border-radius: 100rpx;

		}
	}

	.listViewIcon {
		width: 54rpx;
		vertical-align: middle;
	}

	.contentBox {
		height: 200rpx;
		padding-top: 40rpx;
		background-image: linear-gradient(#FFFFFF, #F5F5F4, #FFFFFF, #FFFFFF, #FFFFFF, #FFFFFF, #FFFFFF, );
margin-top: 30rpx;
		.firstBox {
			display: flex;
			margin: 0 20rpx;
			height: 160rpx;

			.leftBox {
				background-color: white;
				padding: 20rpx;
				width: 50%;
				border-radius: 20rpx;
				box-shadow: 0px 4px 20px 0px rgba(8, 8, 8, 0.1);

				.firstLine {
					display: flex;
					justify-content: space-between;

					.icons {
						width: 50rpx;
					}
				}

				.secondLine {
					color: #7F7F7F;
					font-size: 24rpx;

					text:first-child {
						color: #FA5925;
						font-size: 32rpx;
						font-weight: 700;
					}
				}

			}

			.rightBox {
				border-radius: 20rpx;
				padding: 20rpx;
				width: 50%;
				margin-left: 10rpx;
				box-shadow: 0px 4px 20px 0px rgba(8, 8, 8, 0.1);
				background-color: white;

				.firstLine {
					display: flex;
					justify-content: space-between;

					.icons {
						width: 50rpx;
					}
				}

				.secondLine {
					color: #FA5925;
					font-weight: 700;
				}


			}
		}

		.secondBox {
			position: relative;
			margin: 40rpx 24rpx 10rpx 24rpx;
			padding: 20rpx 14rpx;
			border-radius: 22rpx;
			display: flex;
			justify-content: space-between;
			border: 1px solid #DFE3EB;
			background-image: linear-gradient(to right, #F5F6F7, #FFFFFF);
box-shadow: 0px 4px 20px 0px rgba(8, 8, 8, 0.1);
			.rightBox {
				position: absolute;
				top: 50%;
				right: 14rpx;
				transform: translateY(-50%);
				background-color: #FB766A;
				color: white;
				height: 64rpx;
				padding: 0 24rpx;
				border-radius: 10rpx;
				line-height: 64rpx;
				font-size: 28rpx;
			}

			.leftBox {
				padding-left: 14rpx;
				
				font-size: 30rpx;
			}
		}
	}
</style>
