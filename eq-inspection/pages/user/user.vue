<template>
	<view class="content">
		<view class="user-header">
			<img src="../../static/img/userlogin.png" alt="">
			<view class="user-info">
				<view class="userName">{{user.userName}}</view>
				<view class="rask">{{user.state}}</view>
			</view>
			<button type="primary" @tap="bindLogout">注销</button>
		</view>
		<view class="user-items">
			<navigator :url="item.url" v-for="item in itemslist" :key="item.index">
				<view class="changepwd item">
					<img :src="item.imgSrc" alt="">
					<view>{{item.itemName}}</view>
					<img src="../../static/img/right.png" alt="" class="arrow">
				</view>
			</navigator>
		</view>
	</view>
</template>

<script>
	import {
		mapState,
		mapMutations
	} from 'vuex'

	export default {
		data(){
			return{
				itemslist:[{
					imgSrc:'../../static/img/make.png',
					itemName:'我的排班',
					url:'../inspection/inspection'
					},{
					imgSrc:'../../static/img/cpwd.png',
					itemName:'修改密码',
					url:'../changepwd/changepwd'
					},{
					imgSrc:'../../static/img/about.png',
					itemName:'关于我们',
					url:''
				}],
				user:{
					userName:'赵铁柱',
					state:'您今天还没有工作安排'
					}
			}
		},
		computed: {
			...mapState(['hasLogin', 'forcedLogin'])
		},
		methods: {
			...mapMutations(['logout']),
			bindLogout() {
				var that = this;
				uni.showModal({
				    title: '提示',
				    content: '是否确认退出登录',
				    success: function (res) {
				        if (res.confirm) {
				           that.logout();
				           if (that.forcedLogin) {
				           	uni.reLaunch({
				           		url: '../login/login',
				           	});
				           }
				        } else if (res.cancel) {
				            console.log('用户点击取消');
				        }
				    }
				});
				
			},
			
		}
	}
</script>

<style lang="scss">
	@import "../../static/css/color.scss";
	.user-header {
		display: flex;
		justify-content: center;
		align-items: center;
		background: #FFFFFF;
		padding: 30px 10px;

		img {
			width: 50px;
			height: 50px;
		}
		.user-info {
			flex: 1;
			padding: 0 10px;
			margin-left: 20px;
			.userName {
				font-size: 15px;
				padding: 5px 0;
			}
			.rask {
				font-size: 13px;
			}
		}
		uni-button[type=primary] {
			color: $duckBlue;
			background-color: #FFFFFF;
			width: 80px;
			height: 40px;
			line-height: 40px;
			font-size: 13px;
		}
	}
	.user-items {
		margin-top: 5px;
		.item {
			display: flex;
			justify-content: center;
			align-items: center;
			background: #FFFFFF;
			padding: 15px 10px;
			margin-bottom: 1px;
			font-size: 14px;
			img {
				width: 40px;
				height: 40px;
				margin-left: 10px;
			}
			view {
				margin-left: 30px;
				flex: 1;
			}
			.arrow {
				width: 30px;
				height: 30px;
			}
		}
	}
</style>
