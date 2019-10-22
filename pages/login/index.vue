<template>
	<view class="login">
		<view class="content">
			<view class="login-form">
				<view class="item phone">
					<input class="uni-input" v-model="nickname" placeholder="用户名" placeholder-class="input-placeholder"/>
				</view>
				<view class="item password">
					<input class="uni-input" v-model="password" placeholder="密码" type="password" placeholder-class="input-placeholder"/>
				</view>
				<view class="btn" @click="login">
					<text>登录</text>
				</view>
				<view class="forgot-pwd"><text>忘记密码？</text></view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				nickname: '',
				password:''
			}
		},
		methods: {
			login(){
				if(this.nickname && this.password){
					uni.setStorage({
						key: 'userinfo',
						data: {
							nickname: this.nickname,
							thumb: 'https://avatars1.githubusercontent.com/u/13494930?s=120&v=4'
						},
						success() {
							uni.navigateBack();
						}
					})
				}else{
					uni.showToast({
					    title: '请输入用户名和密码',
						icon: 'none'
					});
				}
			}
		}
	}
</script>

<style scoped>
	.content {position: absolute; top: 0;width: 100%;}
	.login-form {width: 630rpx; margin: 50px auto;}
	.login-form .item {
		width: 630rpx;
		height: 84rpx;
		border-radius: 6rpx;
		margin-bottom: 33rpx;
		display: flex;
		justify-content: space-around;
		align-items: center;
		background-color: #eee;
	}
	.login-form input {color: #222; width: 92%; height: 84rpx; line-height: 84rpx;}
	.input-placeholder {color: #999; line-height: 84rpx; height: 84rpx; margin: auto;}
	.login-form .btn{ margin: 43rpx auto 22rpx auto;
		text-align: center;
		height: 84rpx;
		line-height: 84rpx;
		border-radius: 6rpx;
		background-color: #AB956D;
	}
	.forgot-pwd {text-align: right;}
	.login-third .text{margin: 137rpx auto 106rpx auto; text-align: center; }
	
	.login-third .flex{text-align: center; display: flex; justify-content: space-around; }
	.login-third .flex image {width: 88rpx; height: 88rpx;}
	text{
		height: 30rpx;
		font-family: PingFang-SC-Regular;
		font-size: 32rpx;
		font-weight: bold;
		font-stretch: normal;
		line-height: 40rpx;
		letter-spacing: 3rpx;
		color: #ffffff;
	}
</style>
