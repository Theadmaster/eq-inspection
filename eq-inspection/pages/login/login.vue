<template>
    <view class="content">
        <view class="input-group">
            <view class="input-row border">
                <text class="title">账号：</text>
				<input class="m-input" type="text" v-model="account" placeholder="手机号/邮箱/员工号" @blur="checkUserName()">             
            </view>
			<view v-if="isExit" class="user-tips">当前用户不存在</view>
            <view class="input-row">
                <text class="title">密码：</text>
                <m-input type="password" displayable v-model="password" placeholder="密码"></m-input>
            </view>
        </view>
		   <view class=" mui-input-row mui-checkbox ">
		            <checkbox-group >
		                <checkbox
		                    id="chkRem"
		                    type="checkbox"
		                    :checked="rememberPsw"
		                    @tap="rememberPsw = !rememberPsw" color="#FFCC33"
		                    class="RememberCheck"	
		                >
		                    记住密码
		                </checkbox>
		            </checkbox-group>
		        </view>
        <view class="btn-row">
            <button type="primary" class="primary" @tap="bindLogin">登录</button>
        </view>
        <view class="action-row">
            <navigator url="../pwd/pwd">忘记密码</navigator>
        </view>		
    </view>
</template>

<script>
    import service from '../../service.js';
    import {
        mapState,
        mapMutations
    } from 'vuex'
    import mInput from '../../components/m-input.vue'

    export default {
        components: {
            mInput
        },
        data() {
            return {
                providerList: [],
                hasProvider: false,
                account: '',
                password: '',
                positionTop: 0,
				isExit:false,
				rememberPsw:false
            }
        },
		
		computed: mapState(['forcedLogin']),
        methods: {
			bindLogin(){
				if(true){
					//登录成功将用户名密码存储到用户本地
					if(this.rememberPsw){//用户勾选“记住密码”
						uni.setStorageSync('userName', this.account);
						uni.setStorageSync('password', this.password);
					}else{//用户没有勾选“记住密码”
						uni.removeStorageSync('userName');
						uni.removeStorageSync('password');
						this.account = "";
						this.password= "";
					}	
					
					uni.switchTab({
						url:'../main/main'
					})
				}else{
					uni.showToast({
						title:'失败'
					})
				}
			},
			checkUserName(){
				this.isExit = true;
				console.log(123)
			}
        },
        onReady() {
          let that = this;
          //页面加载完成，获取本地存储的用户名及密码
          const userName = uni.getStorageSync('userName');
          const userPsw = uni.getStorageSync('password');
		  console.log(userName+'xxx')
          if(userName && userPsw){
          	that.account = userName;
          	that.password = userPsw;
			that.rememberPsw = true;
          }else{
          	that.account = "";
          	that.password = "";
          }
        }
    }
</script>

<style lang="scss">
	.content{
		background: url(../../static/img/login.png) no-repeat left top;
		background-size:100% 100%;
		padding: 30px;
		font-size: 13px;
		.input-group{
			margin-top: 170px;
			margin-bottom: 30px;
			background-color: transparent;
			color: #d0e5e9;
			border: none;
			::before {
				height: 0;
			}
			.m-input{
				border: none;
				padding: 10px;
			}
			.user-tips{
				font-size: 12px;
				color: red;
				position: absolute;
			}
		}
		.input-row.border::after{
			left: 0;
		}
		.mui-input-row{
			padding-left: 15px;
			checkbox{
				color: #D0E5E9;
			}
		}
		uni-checkbox .uni-checkbox-input {
			height: 12px;
			width: 12px;
			color:#FFFFFF
		}
		.action-row {
		    display: flex;
		    flex-direction: row;
		    justify-content: center;
			navigator {
			    color: #FFFFFF;
			    padding: 0 20upx;
			}
		}
		.btn-row{
			margin-top: 70px;
			button{
				background: #74b8db;
				color: #4b6176;
			}
		}
	}
</style>
