<template>
	<view>
		<!-- #ifdef MP-WEIXIN -->
		<view class="navBox">
			<text>订单</text>
		</view>
		<!-- #endif -->

		<s-tabs effect @change="change" @render="render" activeColor="black" barColor="#FB766A" barHeight=8 barWidth=50>
			<s-tab v-for="(item,index) in tabList" :title="item" :key="index">
				<view class="contentBox">
					<image src="../../static/cart/nothing.jpg" class="nothingImg"></image>
					<view class="tips">近一年没有订单</view>
					<view class="tipsButton" @click="pushHome">去下单</view>
				</view>
			</s-tab>
		</s-tabs>

	</view>
</template>

<script>
	import sTabs from '../../components/s-tabs/index.vue';
	import sTab from '../../components/s-tab/index.vue';
	export default {
		data() {
			return {
				tabList: ['全部', '待消费', '待评价', '退款', '卡卷订单'],
			}
		},
		components: {
			sTabs,
			sTab
		},
		methods: {
			change(index) {
				console.log('change:', index);
			},
			render(index) {
				console.log('render:', index);
			},
			pushHome() {
				uni.switchTab({
					url: '../home/home'
				});

			}
		}
	}
</script>

<style lang="less">
	page {
		background-color: #F7F7F7;
	}

	.navBox {
		height: 129rpx;
		background-color: #FB766A;
		line-height: 150rpx;
		color: white;
		padding-left: 30rpx;

	}

	.contentBox {
		text-align: center;
		margin-top: 50%;
		position: absolute;
		left: 50%;
		transform: translate(-50%, -50%);
		

		.tips {
			color: #727272;
			font-size: 30rpx;
		}

		.tipsButton {
			width: 100rpx;
			height: 40rpx;
			background-color: #FB766A;
			padding: 10rpx 24rpx;
			border-radius: 40rpx;
			margin: 40rpx auto;
			color: white;
		}
	}
</style>
