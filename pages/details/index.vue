<template>
	<view>
		<view class="goods-box">
			<image :src="goods.image" class="goods-thumb"></image>

			<navigator open-type="switchTab" url="/pages/cart/index">
				<view class="carts-icon" :class="{'on':scaleCart}">
					<image src="/static/image/cart2.png"></image>
					<text class="carts-icon-num" v-if="hasCarts">{{totalNum}}</text>
				</view>
			</navigator>

			<view class="goods-operation">
				<text class="goods-operation-num">数量 {{num}}</text>
				<text class="goods-operation-add" @click="addCount">+</text>
				<text class="goods-to-cart" @click="addToCart">加入购物车</text>
				<image src="/static/image/cart1.png" class="goods-cart-img" @click="addToCart"></image>
			</view>
			<image v-if="show" src="/static/image/cart1.png" class="to-carts-icon"></image>
			<view class="goods-stock">{{goods.stock}}</view>
			<view class="goods-title">{{goods.title}}</view>
			<view class="goods-price">￥ {{goods.price}}</view>
		</view>
		<view class="goods-tab-box">
			<view class="goods-tab-nav" :class="{'on':curIndex===0}" @click="bindTap" data-index="0">商品详情</view>
			<view class="goods-tab-nav" :class="{'on':curIndex===1}" @click="bindTap" data-index="1">产品参数</view>
			<view class="goods-tab-nav" :class="{'on':curIndex===2}" @click="bindTap" data-index="2">售后保障</view>
			<view class="goods-content">
				<view v-if="curIndex === 0">{{goods.detail}}</view>
				<view v-if="curIndex === 1">{{goods.parameter}}</view>
				<view v-if="curIndex === 2">{{goods.service}}</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				goods: {
					id: 1,
					image: '/static/image/goods1.png',
					title: '新鲜梨花带雨',
					price: 0.01,
					stock: '有货',
					detail: '这里是梨花带雨详情。',
					parameter: '125g/个',
					service: '不支持退货'
				},
				num: 1,
				totalNum: 0,
				hasCarts: false,
				curIndex: 0,
				show: false,
				scaleCart: false
			}
		},
		methods: {
			addCount() {
				this.num++;
			},

			addToCart() {
				const num = this.num;
				let total = this.totalNum;
				this.show = true;
				setTimeout(() => {
					this.show = false;
					this.scaleCart = true;
					setTimeout(() => {
						this.scaleCart = false;
						this.hasCarts = true;
						this.totalNum = num + total;
					}, 200)
				}, 300)

			},

			bindTap(e) {
				const index = parseInt(e.currentTarget.dataset.index);
				this.curIndex = index;
			}
		}
	}
</script>

<style>
	.goods-box {
		position: relative;
		padding: 40rpx 45rpx;
		text-align: center;
		color: #454552;
		border-bottom: 30rpx solid #ededed;
	}

	.goods-box .goods-thumb {
		width: 300rpx;
		height: 300rpx;
		margin: 35rpx 0 125rpx;
	}

	.to-carts-icon {
		position: absolute;
		right: 70rpx;
		top: 70rpx;
		width: 10rpx;
		height: 10rpx;
		border-radius: 50%;
		opacity: .6;
		-webkit-animation: to_cart .3s ease-out;
		animation: to_cart .3s ease-out;
	}

	@-webkit-keyframes to_cart {
		0% {
			right: 100rpx;
			top: 530rpx;
			-webkit-transform: scale(4);
		}

		/*60%{
	        top: 20rpx;
	    }*/
	}

	@keyframes to_cart {
		0% {
			right: 100rpx;
			top: 530rpx;
			transform: scale(4);
		}

		/*60%{
	        top: 20rpx;
	    }*/
	}

	.carts-icon {
		position: absolute;
		right: 40rpx;
		top: 40rpx;
		width: 75rpx;
		height: 75rpx;
	}

	.carts-icon image {
		width: 100%;
		height: 100%;
	}

	.carts-icon.on {
		-webkit-animation: to_cart_scale .3s ease;
		animation: to_cart_scale .3s ease;
	}

	@-webkit-keyframes to_cart_scale {
		50% {
			-webkit-transform: scale(1.2);
		}
	}

	@keyframes to_cart_scale {
		50% {
			transform: scale(1.2);
		}
	}

	.carts-icon-num {
		position: absolute;
		left: -15rpx;
		width: 40rpx;
		height: 40rpx;
		line-height: 40rpx;
		border-radius: 50%;
		background: #AB956D;
		color: #fff;
		font-size: 24rpx;
	}

	.goods-box .goods-operation {
		position: relative;
		width: 100%;
		height: 100rpx;
		line-height: 100rpx;
		padding: 0 50rpx;
		margin-bottom: 60rpx;
		box-sizing: border-box;
		border-radius: 50rpx;
		background: #AB956D;
		color: #fff;
		font-size: 28rpx;
	}

	.goods-operation text {
		display: inline-block;
		height: 100rpx;
	}

	.goods-operation-num {
		width: 160rpx;
	}

	.goods-operation-add {
		width: 80rpx;
		margin-right: 30rpx;
	}

	.goods-to-cart {
		width: 210rpx;
		padding-right: 75rpx;
	}

	.goods-cart-img {
		position: absolute;
		right: 50rpx;
		top: 28rpx;
		width: 45rpx;
		height: 45rpx;
	}

	.goods-stock {
		font-size: 28rpx;
		margin-bottom: 20rpx;
	}

	.goods-title {
		font-size: 40rpx;
		margin-bottom: 30rpx;
	}

	.goods-price {
		font-size: 40rpx;
	}

	.goods-tab-nav {
		display: inline-block;
		width: 33.33%;
		height: 90rpx;
		line-height: 90rpx;
		border-bottom: 1rpx solid #ededed;
		box-sizing: border-box;
		text-align: center;
		color: #c7c7cb;
	}

	.goods-tab-nav.on {
		color: #bcaa8a;
		border-bottom: 5rpx solid #bcaa8a;
	}

	.goods-content {
		padding: 40rpx;
	}
</style>
