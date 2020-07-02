<template>
	<view class="content">
		<view class="main-header">
			<view class="task-number">{{alreadyTask}} / {{allTask}}</view>
			<view class="main-title">已检/需检</view>
			<view class="now-time">{{nowTime}}</view>
		</view>
		<view class="main-items">
			<navigator :url="item.url" v-for="item in itemslist" :key="item.index">
				<view class="schedule item">
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
		mapState
	} from 'vuex'

	export default {
		data() {
		    return {
				alreadyTask:'5',
				allTask:'20',
		        nowTime: '2020/04/02',
				itemslist:[{
					imgSrc:'../../static/img/xun.png',
					itemName:'我的巡检',
					url:'../inspection/inspection'
					},{
					imgSrc:'../../static/img/fu.png',
					itemName:'我的复检',
					url:''
					},{
					imgSrc:'../../static/img/enignee.png',
					itemName:'设备列表',
					url:''
				}]
		    }
		},
		computed: mapState(['forcedLogin', 'hasLogin', 'userName']),
		onLoad() {
		}
	}
</script>

<style lang="scss">
	@import "../../static/css/color.scss";	
	.main-header{
		background: #7aabc4;
		height: 180px;
		color: #FFFFFF;
		position: relative;
		font-size: 15px;
		.task-number{
			text-align: center;
			margin-top: 40px;
			font-size: 25px;
		}
		.main-title{
			background: #FFFFFF;
			color: $duckBlue;
			width: 130px;
			margin: 20px auto;
			padding: 10px 20px;
			text-align: center;
			border-radius: 20px;
		}
		.now-time{
			position: absolute;
			bottom: 10px;
			right: 10px;
		}
	}
	.main-items{
		.item{
			display: flex;
			justify-content: center;
			align-items: center;
			background: #FFFFFF;
			padding: 15px 10px;
			margin-bottom: 1px;
			font-size: 14px;
			img{
				width: 40px;
				height: 40px;
				margin-left: 10px;
			}
			view{
				margin-left: 30px;
				flex: 1;
			}
			.arrow{
				width: 30px;
				height: 30px;
			}
		}
	}
</style>
