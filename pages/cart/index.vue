<template>
	<view>
		<view v-if="hasList">
			<view class="cart-box">
				<view class="cart-list" v-for="(item,index) in carts" :key="index">
					<view v-if="item.selected" class="cart-pro-select" :data-index="index" @click="selectList">
						<image src="/static/image/select.png"></image>
					</view>
					<view v-else class="cart-pro-select no-select" :data-index="index" @click="selectList"></view>
					<navigator url="/pages/details/index">
						<image class="cart-thumb" :src="item.image"></image>
					</navigator>
					<text class="cart-pro-name">{{item.title}}</text>
					<text class="cart-pro-price">￥{{item.price}}</text>
					<view class="cart-count-box">
						<text class="cart-count-down" @click="minusCount" data-obj="obj" :data-index="index">-</text>
						<text class="cart-count-num">{{item.num}}</text>
						<text class="cart-count-add" @click="addCount" :data-index="index">+</text>
					</view>
					<text class="cart-del" @click="deleteList" :data-index="index">×</text>
				</view>
			</view>

			<view class="cart-footer">
				<!-- <icon v-if="selectAllStatus" type="success_circle" color="#fff" class="total-select" @click="selectAll" />
				<icon wx:else type="circle" color="#fff" class="total-select" @click="selectAll" /> -->
				<view v-if="selectAllStatus" class="total-select" @click="selectAll">
					<image src="/static/image/select1.png"></image>
				</view>
				<view v-else class="total-select no-select" @click="selectAll"></view>
				<view class="order-icon">
					<navigator url="/pages/orders/index">
						<image src="/static/image/icon3.png"></image>
					</navigator>
				</view>
				<text>全选</text>
				<text class="cart-toatl-price">￥{{totalPrice}}</text>
			</view>
		</view>
		<view v-else>
			<view class="cart-no-data">购物车是空的哦~</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				carts: [{
						id: 1,
						title: '新鲜芹菜 半斤',
						image: '/static/image/s5.png',
						num: 4,
						price: 0.01,
						selected: true
					},
					{
						id: 2,
						title: '素米 500g',
						image: '/static/image/s6.png',
						num: 1,
						price: 0.03,
						selected: true
					}
				], // 购物车列表
				hasList: true, // 列表是否有数据
				totalPrice: 0, // 总价，初始为0
				selectAllStatus: true, // 全选状态，默认全选
				obj: {
					name: "hello"
				}
			}
		},
		onLoad() {
			this.getTotalPrice();
		},
		methods: {
			/**
			 * 当前商品选中事件
			 */
			selectList(e) {
				console.log(111111)
				const index = e.currentTarget.dataset.index;
				let carts = this.carts;
				const selected = carts[index].selected;
				carts[index].selected = !selected;
				this.carts = carts;
				this.getTotalPrice();
			},

			/**
			 * 删除购物车当前商品
			 */
			deleteList(e) {
				const index = e.currentTarget.dataset.index;
				let carts = this.carts;
				carts.splice(index, 1);
				this.carts = carts;
				if (!carts.length) {
					this.hasList = false;
				} else {
					this.getTotalPrice();
				}
			},

			/**
			 * 购物车全选事件
			 */
			selectAll(e) {
				console.log(111111)
				let selectAllStatus = this.selectAllStatus;
				selectAllStatus = !selectAllStatus;
				let carts = this.carts;

				for (let i = 0; i < carts.length; i++) {
					carts[i].selected = selectAllStatus;
				}
				this.selectAllStatus = selectAllStatus;
				this.carts = carts;
				this.getTotalPrice();
			},

			/**
			 * 绑定加数量事件
			 */
			addCount(e) {
				const index = e.currentTarget.dataset.index;
				let carts = this.carts;
				let num = carts[index].num;
				num = num + 1;
				carts[index].num = num;
				this.carts = carts;
				this.getTotalPrice();
			},

			/**
			 * 绑定减数量事件
			 */
			minusCount(e) {
				console.log(e.currentTarget)
				const index = e.currentTarget.dataset.index;
				const obj = e.currentTarget.dataset.obj;
				let carts = this.carts;
				let num = carts[index].num;
				if (num <= 1) {
					return false;
				}
				num = num - 1;
				carts[index].num = num;
				this.carts = carts;
				this.getTotalPrice();
			},

			/**
			 * 计算总价
			 */
			getTotalPrice() {
				let carts = this.carts; // 获取购物车列表
				let total = 0;
				for (let i = 0; i < carts.length; i++) { // 循环列表得到每个数据
					if (carts[i].selected) { // 判断选中才会计算价格
						total += carts[i].num * carts[i].price; // 所有价格加起来
					}
				}
				this.carts = carts;
				this.totalPrice = total.toFixed(2);
			}
		}
	}
</script>

<style>
	.cart-box {
		padding-bottom: 100rpx;
	}

	.cart-list {
		position: relative;
		padding: 20rpx 20rpx 20rpx 285rpx;
		height: 185rpx;
		border-bottom: 1rpx solid #e9e9e9;
	}

	.cart-list .cart-pro-select {
		position: absolute;
		left: 20rpx;
		top: 90rpx;
		width: 44rpx;
		height: 44rpx;
	}
	
	.cart-list .cart-pro-select image{
		width: 100%;
		height: 100%;
	}
	.cart-list .cart-pro-select.no-select{
		box-sizing: border-box;;
		border: 1px solid #999;
		border-radius: 50%;
	}

	.cart-list .cart-thumb {
		position: absolute;
		top: 20rpx;
		left: 85rpx;
		width: 185rpx;
		height: 185rpx;
	}

	.cart-list .cart-pro-name {
		display: inline-block;
		width: 300rpx;
		height: 105rpx;
		line-height: 50rpx;
		overflow: hidden;
	}

	.cart-list .cart-pro-price {
		display: inline-block;
		float: right;
		height: 105rpx;
		line-height: 50rpx;
	}

	.cart-list .cart-count-box {
		position: absolute;
		left: 285;
		bottom: 20rpx;
		width: 250rpx;
		height: 80rpx;
	}

	.cart-list .cart-count-box text {
		display: inline-block;
		line-height: 80rpx;
		text-align: center;
	}

	.cart-count-down,
	.cart-count-add {
		font-size: 44rpx;
		width: 50rpx;
		height: 100%;
	}

	.cart-count-num {
		width: 150rpx;
	}

	.cart-del {
		position: absolute;
		right: 20rpx;
		bottom: 20rpx;
		width: 80rpx;
		height: 80rpx;
		line-height: 80rpx;
		text-align: center;
		font-size: 44rpx;
	}

	.cart-footer {
		position: fixed;
		bottom: var(--window-bottom);
		left: 0;
		width: 100%;
		height: 90rpx;
		line-height: 90rpx;
		padding: 0 100rpx 0 80rpx;
		box-sizing: border-box;
		background: #AB956D;
		color: #fff;
	}

	.total-select {
		position: absolute;
		left: 20rpx;
		top: 25rpx;
		width: 44rpx;
		height: 44rpx;
	}
	.total-select image{
		width: 100%;
		height: 100%;
		display: block;
	}
	.total-select.no-select{
		box-sizing: border-box;
		border: 1px solid #fff;
		border-radius: 50%;
	}

	.order-icon {
		position: absolute;
		right: 40rpx;
		top: 25rpx;
		width: 45rpx;
		height: 45rpx;
	}

	.order-icon image,
	.order-icon navigator {
		display: block;
		width: 45rpx;
		height: 45rpx;
	}

	.cart-toatl-price {
		float: right;
		width: 120rpx;
	}

	.cart-no-data {
		padding: 40rpx 0;
		color: #999;
		text-align: center;
	}
</style>
