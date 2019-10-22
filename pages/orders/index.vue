<template>
	<view>
		<navigator url="/pages/address/index">
			<view v-if="hasAddress" class="orders-address">
				<text class="orders-address-name">收货人: {{address.name}}</text>
				<text class="orders-address-phone">电话: {{address.phone}}</text>
				<view class="orders-address-detail">{{address.detail}}</view>
			</view>
			<view v-else class="orders-no-address">添加收货地址</view>
		</navigator>

		<view class="orders-box">
			<view v-for="(item, index) in orders" :key="index" class="orders-list">
				<image class="orders-thumb" :src="item.image"></image>
				<view class="orders-pro-name">{{item.title}}</view>
				<view class="orders-pro-price">￥{{item.price}}</view>
				<view class="orders-count-num">×{{item.num}}</view>
			</view>
		</view>

		<view class="orders-footer">
			<view class="orders-footer-total">付款合计：￥{{total}}</view>
			<view class="orders-footer-btn" @click="toPay">去付款</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				address: {},
				hasAddress: false,
				total: 0,
				orders: [{
						id: 1,
						title: '新鲜芹菜 半斤',
						image: '/static/image/s5.png',
						num: 4,
						price: 0.01
					},
					{
						id: 2,
						title: '素米 500g',
						image: '/static/image/s6.png',
						num: 1,
						price: 0.03
					}
				]
			}
		},
		onLoad() {
			this.getTotalPrice();
			uni.getStorage({
				key: 'address',
				success:(res)=> {
					this.address = res.data;
					this.hasAddress = true;
				}
			})
		},
		methods: {
			getTotalPrice() {
				let orders = this.orders;
				let total = 0;
				for (let i = 0; i < orders.length; i++) {
					total += orders[i].num * orders[i].price;
				}
				this.total = total;
			},

			toPay() {
				uni.showModal({
					title: '提示',
					content: '本系统只做演示，支付请调用uni.requestPayment',
				})
			}
		}
	}
</script>

<style>
	.orders-address {
		position: relative;
		padding: 20rpx 50rpx 20rpx 35rpx;
		font-size: 14px;
		line-height: 25px;
		border-bottom: 20rpx solid #ededed;
		color: #adadad;
	}

	.orders-address::after {
		position: absolute;
		right: 30rpx;
		top: 60rpx;
		content: '';
		width: 8px;
		height: 8px;
		border-top: 4rpx solid #7f7f7f;
		border-right: 4rpx solid #7f7f7f;
		-webkit-transform: rotate(45deg);
		transform: rotate(45deg);
	}

	.orders-address-name {
		display: inline-block;
		width: 300rpx;
	}

	.orders-no-address {
		position: relative;
		height: 90rpx;
		line-height: 90rpx;
		color: #adadad;
		border-bottom: 20rpx solid #ededed;
		text-align: center;
	}

	.orders-no-address::after {
		position: absolute;
		right: 30rpx;
		top: 34rpx;
		content: '';
		width: 16rpx;
		height: 16rpx;
		border-top: 4rpx solid #7f7f7f;
		border-right: 4rpx solid #7f7f7f;
		-webkit-transform: rotate(45deg);
		transform: rotate(45deg);
	}

	.orders-box {
		padding-bottom: 105rpx;
	}

	.orders-list {
		position: relative;
		padding: 20rpx 20rpx 20rpx 220rpx;
		height: 180rpx;
		border-bottom: 1rpx solid #ededed;
	}

	.orders-thumb {
		position: absolute;
		top: 20rpx;
		left: 20rpx;
		width: 180rpx;
		height: 180rpx;
	}

	.orders-list view {
		line-height: 60rpx;
	}

	.orders-footer {
		position: fixed;
		bottom: 0;
		left: 0;
		width: 100%;
		height: 95rpx;
		line-height: 95rpx;
		border-top: 1rpx solid #ededed;
	}

	.orders-footer .orders-footer-total {
		display: inline-block;
		width: 510rpx;
		padding-left: 30rpx;
		box-sizing: border-box;
		color: #a55350;
	}

	.orders-footer .orders-footer-btn {
		display: inline-block;
		width: 240rpx;
		text-align: center;
		color: #fff;
		background: #AB956D;
	}
</style>
