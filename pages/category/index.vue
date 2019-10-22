<template>
	<view class="main">
		<view class="categroy-left">
			<view v-for="(item,index) in category" :key="index" :data-id="item.id" @click="switchTab" class="cate-list"
			 :class="{'on':item.id === toView}">{{item.name}}</view>
		</view>

		<scroll-view class="categroy-right" :scroll-y="isScroll" :scroll-into-view="toView" :scroll-with-animation="true">
			<block v-for="(item,idx) in detail" :key="idx">
		            <view :id="item.id" class="cate-box" :style="{'height': height}">
		                <view class="cate-banner">
		                    <image src="/static/image/c1.png"></image>
		                </view>
		                <view class="cate-title">
		                    <text>{{item.cate}}</text>
		                </view>
		                <view class="product">
		                    <view class="product-list" v-for="(val,index) in item.detail" :key="index" >
		                        <navigator url="/pages/list/index">
		                            <image :src="val.thumb"></image>
		                            <view class="classname"><text>{{val.name}}</text></view>
		                        </navigator>
		                    </view>
		                </view>
		            </view>
		        </block>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				category: [{
						name: '果味',
						id: 'guowei'
					},
					{
						name: '蔬菜',
						id: 'shucai'
					},
					{
						name: '炒货',
						id: 'chaohuo'
					},
					{
						name: '点心',
						id: 'dianxin'
					},
					{
						name: '粗茶',
						id: 'cucha'
					},
					{
						name: '淡饭',
						id: 'danfan'
					}
				],
				detail: [
					{
							cate: '果味',
							id: 'guowei',
							detail: [
								{
									thumb: '/static/image/c2.png',
									name: '梨花带雨 3个'
								}
							]
						},
						{
							cate: '蔬菜',
							id: 'shucai',
							detail: [
								{
									thumb: '/static/image/s5.png',
									name: '芹菜 半斤'
								}
							]
						},
						{
							cate: '炒货',
							id: 'chaohuo',
							detail: [
								{
									thumb: '/static/image/s4.png',
									name: '瓜子 100g'
								}
							]
						},
						{
							cate: '点心',
							id: 'dianxin',
							detail: [
								{
									thumb: '/static/image/c2.png',
									name: '梨花带雨 3个'
								}
							]
						},
						{
							cate: '粗茶',
							id: 'cucha',
							detail: [
								{
									thumb: '/static/image/c2.png',
									name: '梨花带雨 3个'
								}
							]
						},
						{
							cate: '淡饭',
							id: 'danfan',
							detail: [
								{
									thumb: '/static/image/s6.png',
									name: '素米 375g'
								}
							]
						}
				],
				curIndex: 0,
				isScroll: false,
				toView: 'guowei',
				height: '100%'
			}
		},
		onLoad() {
			// #ifdef H5
			this.height = document.body.clientHeight-50+'px';
			// #endif
		},
		methods: {
			switchTab(e) {
				this.isScroll = true;
				setTimeout(() => {
					this.toView = e.target.dataset.id;
				}, 0)
				setTimeout(() => {
					this.isScroll = false;
				}, 1)
			}
		}
	}
</script>

<style>
	page,
	.main {
		height: 100%;
	}

	.categroy-left {
		float: left;
		width: 150rpx;
		height: 100%;
		border-right: 1px solid #ddd;
		box-sizing: border-box;
	}

	.categroy-left .cate-list {
		height: 90rpx;
		line-height: 90rpx;
		text-align: center;
		border-left: 3px solid #fff;
	}

	.categroy-left .cate-list.on {
		color: #AB956D;
		border-color: #AB956D;
	}

	.categroy-right {
		float: right;
		width: 600rpx;
		height: 100%;
		overflow: hidden;

	}

	.cate-box {
		height: 100%;
		padding: 40rpx;
		box-sizing: border-box;
	}

	.cate-box .cate-banner image {
		display: block;
		width: 100%;
		height: 190rpx;
	}

	.cate-title {
		position: relative;
		height: 30rpx;
		line-height: 30rpx;
		padding: 30rpx 0 55rpx;
		text-align: center;
		color: #AB956D;
		font-size: 28rpx;
	}

	.cate-title::before {
		position: absolute;
		left: 130rpx;
		top: 43rpx;
		content: '';
		width: 70rpx;
		height: 4rpx;
		background: #AB956D;
	}

	.cate-title::after {
		position: absolute;
		right: 130rpx;
		top: 43rpx;
		content: '';
		width: 70rpx;
		height: 4rpx;
		background: #AB956D;
	}

	.product-list {
		display: inline-block;
		width: 160rpx;
		height: 160rpx;
		text-align: center;
		margin: 0 20rpx 20rpx 0;
		font-size: 24rpx;
	}

	.product-list image {
		width: 80rpx;
		height: 80rpx;
		margin-bottom: 20rpx;
	}

	.product-list:nth-child(3n) {
		margin-right: 0;
	}
</style>
