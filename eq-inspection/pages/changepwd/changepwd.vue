<template>
	<view class="content">
		<view class="input-group">
			<view class="input-row">
				<text class="title">旧密码</text>
				<m-input type="text" focus clearable v-model="oldpwd" placeholder="请输入旧的密码"></m-input>
			</view>
		</view>
		<view class="input-group">
			<view class="input-row">
				<text class="title">新密码</text>
				<m-input type="text" focus clearable v-model="password" placeholder="请输入新的密码"></m-input>
			</view>
		</view>
		<view class="input-group">
			<view class="input-row">
				<text class="title">确认密码</text>
				<m-input type="text" focus clearable v-model="againpwd" placeholder="请再次确认密码"></m-input>
			</view>
		</view>
		<view class="btn-next">
			<button type="primary" class="primary" @tap="findPassword">完成</button>
		</view>
	</view>
</template>

<script>
	import service from '../../service.js';
	import mInput from '../../components/m-input.vue';

	export default {
		components: {
			mInput
		},
		data() {
			return {
				password: '',
				againpwd: '',
				oldpwd: '',
				count: 3,
			}
		},
		methods: {
			findPassword() {
				var patrn = /^(([a-zA-Z]+[0-9]+)|([0-9]+[a-zA-Z]+)|([a-z]+[@#%.])|([0-9]+[@#%.]))([a-zA-Z0-9@#%.]*){6,18}$/;
				if (!patrn.exec(this.password)) {
					uni.showToast({
						icon:'none',
						title:'请输入6-18位字符,至少包含两种字符'
					})
					return ;
				}
				if(this.password!=this.againpwd){
					uni.showToast({
						icon:'none',
						title:'两次密码输入不一致'
					})
					return;
				}

				this.changePassword()
			},
			changePassword() {
				uni.showToast({
					icon:'none',
					title: '修改成功！3秒后自动跳转重新登录'
				})
				this.threeGo()

			},
			threeGo() {
				const TIME_COUNT = 3;
				if (!this.timer) {
					this.count = TIME_COUNT;
					this.show = false;
					this.timer = setInterval(() => {
						if (this.count > 0 && this.count <= TIME_COUNT) {
							this.count--;
						} else {
							this.show = true;
							clearInterval(this.timer);
							this.timer = null;
							uni.navigateTo({
								url: '../login/login'
							})
						}
					}, 1000)
				}
			}
		},
	}
</script>

<style lang="scss">
	@import "../../static/css/color.scss";

	.input-row {
		padding: 11px 0;
		font-size: 13px;
	}

	.uni-input-input {
		font-size: 13px;
	}

	.btn-next {
		position: absolute;
		bottom: 0;
		width: 100%;

		uni-button.primary {
			background-color: $duckBlue;
			line-height: 60px;
			border-radius: 0;
		}
	}
</style>
