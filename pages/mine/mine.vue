<template>
	<view>
		<view class="navBox">
			<text>皮了么</text>
		</view>
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
			font-size: 26rpx;
			.UserName{
				font-size: 44rpx;
				font-weight: 700;
				color: black;
			}
		}

		.rightBox {
			width: 120rpx;
			height: 120rpx;
			overflow: hidden;
			border-radius: 100rpx;

		}
	}
</style>
