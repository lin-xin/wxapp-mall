<template>
	<view>
		<view class="form-box">
			<form @submit="formSubmit">
				<input v-model="address.name" name="name" placeholder="姓名" />
				<input type="number" name="phone" v-model="address.phone" placeholder="电话号码" />
				<input name="detail" v-model="address.detail" placeholder="详细地址" />
				<button form-type="submit">保存</button>
			</form>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				address: {
					name: '',
					phone: '',
					detail: ''
				}
			}
		},
		onLoad() {
			uni.getStorage({
				key: 'address',
				success: (res) => {
					this.address = res.data;
				}
			})
		},
		methods: {
			formSubmit(e) {
				const value = e.detail.value;
				if (value.name && value.phone && value.detail) {
					uni.setStorage({
						key: 'address',
						data: value,
						success() {
							uni.navigateBack();
						}
					})
				} else {
					uni.showModal({
						title: '提示',
						content: '请填写完整资料',
						showCancel: false
					})
				}
			}
		}
	}
</script>

<style>
	.form-box {
		padding-left: 30rpx;
	}

	.form-box input {
		height: 90rpx;
		border-bottom: 1rpx solid #ededed;
		color: #999;
	}

	.form-box .input-placeholder {
		color: #aaa;
	}

	.form-box button {
		margin: 30rpx 30rpx 0 0;
	}
</style>
