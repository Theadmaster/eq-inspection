	<template>
    <view class="content">
        <view class="input-group">
            <view class="input-row">
                <text class="title">手机号</text>
                <m-input type="text" focus clearable v-model="phoneNumber" placeholder="请输入正确的手机"></m-input>
            </view>
        </view>
		<view class="input-check">
			<view class="input-group">
			    <view class="input-row">
			        <text class="title">验证码</text>
			        <m-input type="text" focus clearable v-model="checkNumber" placeholder="请输入验证码"></m-input>
			    </view>
			</view>
			<view class="checkbtn" @tap="getCheckNumber()" :disabled="disabled">{{title}}</view>
		</view>
		<view class="btn-next">
			<button type="primary" class="primary" @tap="nextStep()">下一步</button>
		    
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
                phoneNumber: '',
				checkNumber:'',
				receiveNumber:'123456',
				disabled:false,
				timer:60,
				timer1:'',
				title:'获取',
            }
        },
        methods: {
            findPhoneNumber() {
				var patrn = /^[1][3,4,5,7,8][0-9]{9}$/;
				if(this.phoneNumber===''){
					uni.showToast({
					    icon: 'none',
					    title: '请输入手机号',
					});
					return false;
				}
                if (!patrn.test(this.phoneNumber)) {
                    uni.showToast({
                        icon: 'none',
                        title: '手机号码格式错误',
                    });
                    return false;
                }
				return true;
            },
			getCheckNumber(){
				if(this.findPhoneNumber()){
					let timer1 = setInterval(() => {
						this.timer--;
						this.title='重新获取('+this.timer+'秒)'
						if (this.timer == 0) {
							clearInterval(timer1);
							this.timer = 60;
							this.disabled=false
							this.title='发送验证码'
							return;
						}
					}, 1000);
				}
			},
			nextStep(){
				this.findPhoneNumber()
				
				if(this.checkNumber===''){
					uni.showToast({
					    icon: 'none',
					    title: '请输入验证码',
					});
					return;
				}
				if(this.checkNumber!=this.receiveNumber){
					uni.showToast({
					    icon: 'none',
					    title: '验证码不正确',
					});
					return;
				}
				uni.navigateTo({
					url:'losepwd/losepwd'
				})
			}
        }
    }
</script>

<style lang="scss">
	@import "../../static/css/color.scss";
.input-row{
	padding: 11px 0;
	font-size: 13px;
}
.uni-input-input{
	font-size: 13px;
}
.input-check{
	display: flex;
	width: 100%;
}
.input-check .checkbtn{
	background: #FFFFFF;
	line-height: 59px;
	width: 30%;
	text-align: center;
	font-size: 13px;
	display: inline-block;
	margin-left: 1px;

	flex: 1;
}
.btn-next{
	position: absolute;
	bottom: 0;
	width: 100%;
}

.btn-next uni-button.primary{
	background-color: $duckBlue;
	line-height: 60px;
	border-radius: 0;
}
</style>
