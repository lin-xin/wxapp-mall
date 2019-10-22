<template>
	<view class="content">
		<swiper :indicator-dots="true" :autoplay="true" :interval="interval" :duration="duration" :circular="true">
		        <block v-for="(item,index) in imgUrls" :key="index">
		            <swiper-item>
		                <image :src="item" class="slide-image" width="100%"/>
		            </swiper-item>
		        </block>
		    </swiper>
		    <view class="search">
		        <navigator url="/pages/search/index">
		            <view class="search-text">
		                <icon class="weui-icon-search_in-box search-icon" type="search" size="14"></icon>
		                搜 索
		            </view>
		        </navigator>
		    </view>
		    <view class="selected">
		        <view class="select-title"><text>精选主题</text></view>
		        <view class="select-top">
		            <view class="select-top-small">
		                <navigator url="/pages/list/index">
		                    <image src="/static/image/s1.png"></image>
		                </navigator>
		            </view>
		            <view class="select-top-small">
		                <navigator url="/pages/list/index">
		                    <image src="/static/image/s2.png"></image>
		                </navigator>
		            </view>
		        </view>
		        <view class="select-bottom">
		            <navigator url="/pages/list/index">
		                <image src="/static/image/s3.png"></image>
		            </navigator>
		        </view>
		    </view>
		<view class="newest">
			<view class="newest-title"><text>最近新品</text></view>
			<view class="newest-box">
				<view class="newest-list">
					<navigator url="/pages/details/index">
						<image src="/static/image/s4.png"></image>
						<view class="newest-text"><text>瓜子 100g</text></view>
						<view class="newest-text"><text>￥ 0.01</text></view>
					</navigator>
				</view>
				<view class="newest-list">
					<navigator url="/pages/details/index">
						<image src="/static/image/s5.png"></image>
						<view class="newest-text"><text>芹菜 半斤</text></view>
						<view class="newest-text"><text>￥ 0.02</text></view>
					</navigator>
				</view>
				<view class="newest-list">
					<navigator url="/pages/details/index">
						<image src="/static/image/s6.png"></image>
						<view class="newest-text"><text>素米 375g</text></view>
						<view class="newest-text"><text>￥ 0.03</text></view>
					</navigator>
				</view>
				<view class="newest-list">
					<navigator url="/pages/details/index">
						<image src="/static/image/s4.png"></image>
						<view class="newest-text"><text>瓜子 100g</text></view>
						<view class="newest-text"><text>￥ 0.01</text></view>
					</navigator>
				</view>
				<view class="newest-list">
					<navigator url="/pages/details/index">
						<image src="/static/image/s5.png"></image>
						<view class="newest-text"><text>芹菜 半斤</text></view>
						<view class="newest-text"><text>￥ 0.02</text></view>
					</navigator>
				</view>
				<view class="newest-list">
					<navigator url="/pages/details/index">
						<image src="/static/image/s6.png"></image>
						<view class="newest-text"><text>素米 375g</text></view>
						<view class="newest-text"><text>￥ 0.03</text></view>
					</navigator>
				</view>
				<view class="newest-list">
					<navigator url="/pages/details/index">
						<image src="/static/image/s4.png"></image>
						<view class="newest-text"><text>瓜子 100g</text></view>
						<view class="newest-text"><text>￥ 0.01</text></view>
					</navigator>
				</view>
				<view class="newest-list">
					<navigator url="/pages/details/index">
						<image src="/static/image/s5.png"></image>
						<view class="newest-text"><text>芹菜 半斤</text></view>
						<view class="newest-text"><text>￥ 0.02</text></view>
					</navigator>
				</view>
				<view class="newest-list">
					<navigator url="/pages/details/index">
						<image src="/static/image/s6.png"></image>
						<view class="newest-text"><text>素米 375g</text></view>
						<view class="newest-text"><text>￥ 0.03</text></view>
					</navigator>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				imgUrls: [
				      '/static/image/b1.jpg',
				      '/static/image/b2.jpg',
				      '/static/image/b3.jpg'
				    ],
				title: 'Hello',
				interval: 3000,
            duration: 800
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}
.search{
	width: 95%;
    padding: 20rpx;
}
.search-text{
    display: flex;
    justify-content: center;
    align-items: center;
    height: 50rpx;
    color: #aaa;
    text-align: center;
    border: 1px solid #ddd;
    border-radius: 20rpx;
}
.search-text icon{
    margin-right: 10rpx;
}
swiper {
	width: 100%;
    height: 421.5rpx;
}
swiper-item image {
    width: 100%;
    height: 100%;
}

.select-title,.newest-title{
    width: 100%;
    padding:30rpx 0;
    height: 40rpx;
    color: #AB956D;
    text-align: center;
}
.select-top-small{
    width: 375rpx;
    height: 375rpx;
    float: left;
}
.select-bottom,.select-top{
    width: 100%;
    height: 375rpx;
}
.select-top-small image,.select-bottom image,.select-top-small navigator,.select-bottom navigator{
    display: block;
    width: 100%;
    height: 100%;
}
	.newest-box{
	    padding:0 40rpx;
	}
	.newest-box .newest-list{
	    display: inline-block;
	    width: 325rpx;
	    height: 325rpx;
	    margin:0 20rpx 20rpx 0;
	    border-radius: 10px;
	    text-align: center;
	    background: #f5f6f5;
	}
	.newest-box .newest-list:nth-child(2n){
	    margin-right: 0;
	}
	.newest-box .newest-list image{
	    width: 175rpx;
	    height: 175rpx;
	    margin: 20rpx 0 10rpx;
	}
	.newest-box .newest-list .newest-text{
	    font-size: 32rpx;
	}
</style>
