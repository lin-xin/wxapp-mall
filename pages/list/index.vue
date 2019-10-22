<template>
	<view>
		<view class="banner">
		        <image src="/static/image/list1.png"></image>
		    </view>
		
		    <view class="list-box">
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
</template>

<script>
</script>

<style>
	.banner image{
	    width: 100%;
	    height: 400rpx;
	}
	.list-box{
	    padding: 30rpx 20rpx;
	}
	.newest-list{
	    display: inline-block;
	    width: 347rpx;
	    height: 347rpx;
	    margin:0 15rpx 10rpx 0;
	    border-radius: 10px;
	    text-align: center;
	    background: #f5f6f5;
	}
	.newest-list:nth-child(2n){
	    margin-right: 0;
	}
	.newest-list image{
	    width: 180rpx;
	    height: 180rpx;
	    margin: 30rpx 0 20rpx;
	}
	.newest-list .newest-text{
	    font-size: 32rpx;
	    line-height: 45rpx;
	}
</style>
