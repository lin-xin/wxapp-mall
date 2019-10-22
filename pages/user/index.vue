<template>
	<view>
		<template v-if="auth">
			<view class="header">
				<image :src="thumb" class="thumb"></image>
				<text class="nickname">{{nickname}}</text>
				<text class="about">关于我们</text>
			</view>
			<view class="address-box">
				<view class="address-manage">
					<navigator url="/pages/address/index">地址管理</navigator>
				</view>
				<view v-if="hasAddress" class="address-list">
					<view>{{address.name}}</view>
					<view>{{address.phone}}</view>
					<view>{{address.detail}}</view>
				</view>
			</view>
			<view class="orders-box">
				<view class="orders">我的订单</view>
				<view class="orders-list" v-for="(item,index) in orders" :key="index">
					<view class="orders-number">订单编号：{{item.number}}</view>
					<view class="orders-detail">
						<image :src="item.thumb"></image>
						<view class="">{{item.name}}</view>
						<view class="">{{item.count}}</view>
						<text class="orders-status">{{item.status_text}}</text>
					</view>
					<view class="orders-footer">
						<text>实付：￥{{item.money}}</text>
						<button v-if="item.status===2" size="mini" class="orders-btn" @click="payOrders">付款</button>
					</view>
				</view>
			</view>
		</template>
		<template v-else>
			<!-- #ifdef MP-WEIXIN -->
			<button class="btn-auth" open-type="getUserInfo" @getuserinfo="wxGetUserInfo" withCredentials="true">微信授权获取用户信息</button>
			<!-- #endif -->
			<!-- #ifdef H5 || APP-PLUS-->
			<navigator url="/pages/login/index">
				<button class="btn-auth">登录</button>
			</navigator>
			<!-- #endif -->
		</template>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				auth: false,
				thumb: '',
				nickname: '',
				orders: [{
					number: 'WX347dsh439fg23',
					thumb: '/static/image/s5.png',
					name: '芹菜 3斤',
					count: 1,
					status_text: '已付款',
					status: 1,
					money: 0.03
				}, {
					number: 'WX347dsh439fg24',
					thumb: '/static/image/c2.png',
					name: '素米 1斤',
					count: 1,
					status_text: '待付款',
					status: 2,
					money: 0.01
				}],
				hasAddress: false,
				address: {}
			}
		},
		onShow() {
			// #ifdef H5 || APP-PLUS
			uni.getStorage({
				key: 'userinfo',
				success: (res) => {
					this.auth = true;
					this.nickname = res.data.nickname;
					this.thumb = res.data.thumb;
				}
			})
			// #endif
			this.getAuth();
			uni.getStorage({
				key: 'address',
				success: (res) => {
					this.hasAddress = true;
					this.address = res.data;
				}
			})
		},
		methods: {
			wxGetUserInfo(res) {
				console.log(res)
				if (!res.detail.iv) {
					uni.showToast({
						title: "您取消了授权,登录失败",
						icon: "none"
					});
					return false;
				}
				this.getAuth();
			},
			getAuth(){
				// #ifdef MP-WEIXIN
				uni.authorize({
					scope: 'scope.userInfo',
					success: () => {
						this.auth = true;
						uni.getUserInfo({
							provider: 'weixin',
							success: (infoRes) => {
								this.auth = true;
								this.thumb = infoRes.userInfo.avatarUrl;
								this.nickname = infoRes.userInfo.nickName;
							}
						});
					}
				})
				// #endif
			},
			payOrders() {
				uni.requestPayment({
					timeStamp: 'String1',
					nonceStr: 'String2',
					package: 'String3',
					signType: 'MD5',
					paySign: 'String4',
					success: function(res) {
						console.log(res)
					},
					fail: function(res) {
						wx.showModal({
							title: '支付提示',
							content: '请填写正确的支付配置信息',
							showCancel: false
						})
					}
				})
			}
		}
	}
</script>

<style>
	.btn-auth {
		margin: 20px;
	}

	.header {
		position: relative;
		height: 160rpx;
		line-height: 100rpx;
		padding: 30rpx 30rpx 30rpx 150rpx;
		box-sizing: border-box;
		background: #AB956D;
		font-size: 28rpx;
		color: #fff;
	}

	.header .thumb {
		position: absolute;
		left: 30rpx;
		top: 30rpx;
		width: 100rpx;
		height: 100rpx;
		border-radius: 50%;
	}

	.header .about {
		float: right;
	}

	.address-box {
		border-bottom: 20rpx solid #ededed;
		color: #999;
		line-height: 90rpx;
		font-size: 28rpx;
	}

	.address-box .address-manage {
		position: relative;
		height: 90rpx;
		border-bottom: 1rpx solid #e9e9e9;
		text-align: center;
	}

	.address-box .address-manage::after {
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

	.address-box .address-list {
		padding-left: 30rpx;
	}

	.address-box .address-list view {
		height: 90rpx;
		border-bottom: 1rpx solid #e9e9e9;
	}

	.address-box .address-list view:last-child {
		border-bottom: 0;
	}

	.orders-box {
		color: #999;
		font-size: 28rpx;
	}

	.orders {
		height: 90rpx;
		line-height: 90rpx;
		border-bottom: 1rpx solid #e9e9e9;
		text-align: center;
	}

	.orders-list {
		padding-left: 30rpx;
		border-bottom: 20rpx solid #ededed;
	}

	.orders-list:last-child {
		border-bottom: 0;
	}

	.orders-number {
		height: 90rpx;
		line-height: 90rpx;
		border-bottom: 1rpx solid #e9e9e9;
	}

	.orders-detail {
		position: relative;
		height: 120rpx;
		padding: 35rpx 20rpx 35rpx 170rpx;
		border-bottom: 1rpx solid #e9e9e9;
	}

	.orders-detail image {
		position: absolute;
		left: 0;
		top: 20rpx;
		width: 150rpx;
		height: 150rpx;
	}

	.orders-detail view {
		line-height: 60rpx;
	}

	.orders-detail .orders-status {
		position: absolute;
		right: 20rpx;
		top: 35rpx;
		height: 120rpx;
		line-height: 120rpx;
		color: #b42f2d;
	}

	.orders-footer {
		height: 60rpx;
		line-height: 60rpx;
		color: #2f2f2f;
		padding: 15rpx 30rpx 15rpx 0;
	}

	.orders-footer .orders-btn {
		float: right;
		width: 170rpx;
		height: 60rpx;
		line-height: 60rpx;
		border-radius: 6rpx;
		background: #b42f2d;
		color: #fff;
	}
</style>
