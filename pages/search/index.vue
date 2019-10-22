<template>
	<view class="main">
		<view class="search-box">
			<input class="search-input" placeholder="搜索" :value="value" @input="searchInput" />
			<icon class="weui-icon-search_in-box search-icon" type="search" size="14"></icon>
			<text class="search-btn" v-if="showResult" @click="cancelSearch">取消</text>
		</view>
		<view class="result" v-if="showResult">
			<view class="result-box" v-if="result.length > 0">
				<view class="result-list" v-for="(item,index) in result" :key="index">
					<navigator :url="item.url">
						<image :src="item.thumb"></image>
						<view class="result-text">
							<text>{{item.title}}</text>
						</view>
						<view class="result-text">
							<text>￥ {{item.price}}</text>
						</view>
					</navigator>
				</view>
			</view>
			<view class="result-null" v-else>
				<view class="null-tips">Oh~~ 搜索结果为空！</view>
				<view class="recommend-title">
					<text>相关推荐</text>
				</view>
				<view class="recommend-box">
					<view class="result-list" v-for="(item,index) in result" :key="index">
						<navigator :url="item.url">
							<image :src="item.thumb"></image>
							<view class="result-text">
								<text>{{item.title}}</text>
							</view>
							<view class="result-text">
								<text>￥ {{item.price}}</text>
							</view>
						</navigator>
					</view>
				</view>
			</view>
		</view>
		<view class="init-page" v-else>
			<view v-if="history.length > 0">
				<view class="title">
					<text>搜索记录</text>
				</view>
				<view class="tags">
					<text v-for="(item,index) in history" :key="index" :data-text="item" @click="keywordHandle">{{item}}</text>
				</view>
			</view>
			<view class="title">
				<text>热点推荐</text>
			</view>
			<view class="tags">
				<text v-for="(item,index) in hot" :key="index" :data-text="item" @click="keywordHandle">{{item}}</text>
			</view>
		</view>

		<view class="keywords" v-if="showKeywords">
			<view class="keywords-item" v-for="(item,index) in keywords" :key="index" :data-text="item" @click="keywordHandle">{{item}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				history: [],
				hot: ['新鲜芹菜', '大红枣', '滋补桂圆干'],
				result: [{
						id: 1,
						url: '/pages/details/index',
						thumb: '/static/image/s4.png',
						title: '瓜子 100g',
						price: 0.01
					},
					{
						id: 2,
						url: '/pages/details/index',
						thumb: '/static/image/s5.png',
						title: '新鲜芹菜 500g',
						price: 0.02
					}
				],
				showKeywords: false,
				keywords: ['山东肚脐橙', '湖南冰糖橙', '麻涌香蕉', '冰糖心苹果'],
				value: '',
				showResult: false,
				timeId: null
			}
		},
		onLoad() {
			const history = uni.getStorageSync('history');
			if (history) {
				this.history = JSON.parse(history)
			}
		},
		methods: {
			cancelSearch() {
				this.showResult = false;
				this.showKeywords = false;
				this.value = '';
			},
			searchInput(e) {
				if (!e.detail.value) {
					this.showKeywords = false;
				} else {
					if (!this.showKeywords) {
						this.timeId && clearTimeout(this.timeId);
						this.timeId = setTimeout(() => {
							this.showKeywords = true;
						}, 1000)
					}
				}
			},
			keywordHandle(e) {
				const text = e.target.dataset.text;
				this.value = text;
				this.showKeywords = false;
				this.showResult = true;
				this.historyHandle(text);
			},
			historyHandle(value) {
				let history = this.history;
				const idx = history.indexOf(value);
				if (idx === -1) {
					// 搜索记录只保留8个
					if (history.length > 7) {
						history.pop();
					}
				} else {
					history.splice(idx, 1);
				}
				history.unshift(value);
				uni.setStorageSync('history', JSON.stringify(history));
				this.history = history;
			},
		}
	}
</script>

<style>
	.main {
		padding: 0 20rpx;
	}

	.search-box {
		position: relative;
		display: flex;
		justify-content: space-between;
		padding-top: 26rpx;
	}

	.search-input {
		flex: 1;
		height: 60rpx;
		line-height: 60rpx;
		padding: 0 20rpx 0 54rpx;
		background: #f8f8f8;
		border-radius: 10rpx;
		font-size: 32rpx;
		border: 2rpx solid #ddd;
	}

	.search-icon {
		position: absolute;
		left: 15rpx;
		top: 44rpx;
		width: 35rpx;
		height: 35rpx;
	}

	.search-btn {
		font-size: 32rpx;
		padding: 0 20rpx;
		line-height: 64rpx;
	}

	.title {
		font-size: 32rpx;
		margin: 30rpx 0;
	}

	.title text {
		padding-right: 30rpx;
		padding-bottom: 10rpx;
		color: #AB956D;
		border-bottom: 8rpx solid #AB956D;
	}

	.tags text {
		display: inline-block;
		font-size: 28rpx;
		padding: 6rpx 20rpx;
		border: 2rpx solid #ddd;
		color: #aaa;
		margin: 0 30rpx 20rpx 0;
		border-radius: 40rpx;
		word-break: break-all;
	}

	.keywords {
		position: absolute;
		width: 100%;
		left: 0;
		top: 90rpx;
		background: #fff;
		z-index: 9;
		padding: 20rpx;
		box-sizing: border-box;
	}

	.keywords-item {
		line-height: 70rpx;
		border-bottom: 1px solid #eee;
		color: #787878;
		font-size: 28rpx;
	}

	.result {
		margin-top: 40rpx;
	}

	.result-box,
	.recommend-box {
		padding: 0 20rpx;
	}

	.result-list {
		display: inline-block;
		width: 325rpx;
		height: 325rpx;
		margin: 0 20rpx 20rpx 0;
		border-radius: 10px;
		text-align: center;
		background: #f5f6f5;
	}

	.result-list:nth-child(2n) {
		margin-right: 0;
	}

	.result-list image {
		width: 175rpx;
		height: 175rpx;
		margin: 20rpx 0 10rpx;
	}

	.result-list .result-text {
		font-size: 32rpx;
	}

	.null-tips {
		padding: 200rpx 0;
		text-align: center;
		color: #787878;
	}

	/* 相关推荐 */
	.recommend-title {
		position: relative;
		height: 0;
		width: 1005;
		border-bottom: 1px solid #f0f0f1;
		margin-bottom: 42rpx;
	}

	.recommend-title text {
		position: absolute;
		left: 50%;
		top: -20rpx;
		width: 150rpx;
		height: 40rpx;
		margin-left: -75rpx;
		line-height: 40rpx;
		background: #ffffff;
		color: #5e5e5e;
		font-size: 28rpx;
		font-weight: bold;
		text-align: center;
		letter-spacing: 1px;
	}
</style>
