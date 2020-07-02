<template>
    <view class="content">
        <view class="input-group">
            <view class="input-row">
                <text class="title">新密码</text>
                <m-input type="text" focus clearable v-model="password" placeholder="请输入6-18位字符,至少包含两种字符"></m-input>
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
    import service from '../../../service.js';
    import mInput from '../../../components/m-input.vue';

    export default {
        components: {
            mInput
        },
        data() {
            return {
                password: '',
				againpwd:''
            }
        },
        methods: {
            findPassword() {
				var patrn=/^(([a-zA-Z]+[0-9]+)|([0-9]+[a-zA-Z]+)|([a-z]+[@#%.])|([0-9]+[@#%.]))([a-zA-Z0-9@#%.]*){6,18}$/;
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
			changePassword(){
				uni.navigateTo({
					url:'../../login/login'
				})
			}
        }
    }
</script>

<style lang="scss">
@import "../../../static/css/color.scss";
.input-row{
	padding: 11px 0;
	font-size: 13px;
}
.uni-input-input{
	font-size: 13px;
}
.btn-next{
	position: absolute;
	bottom: 0;
	width: 100%;
	uni-button.primary{
		background-color: $duckBlue;
		line-height: 60px;
		border-radius: 0;
	}
}
</style>
