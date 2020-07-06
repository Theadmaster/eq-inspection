<template>
	<view class="content">
		
		<!-- 顶部导航栏 -->
		<uni-nav-bar 
		background-color="#7aabc4"
		color="white"
		left-icon="back"
		title="巡检点02"
		rightText="完成"
		@clickRight="finish"
		@clickLeft="back"
		>
		</uni-nav-bar>
		
		<!-- 内容 -->
		<view class="wrapper" v-for="(item,index) in targetList" :key="index">
			<!-- <view class="header">
				<icon class="icon-left" type="" />
				<text class="text1">{{item.targetName}}</text>
				<view class="tag">
					<img src="../../../../static/img/tag.png"  />
					<text>当前状态：待巡检</text>
				</view>
				<uni-icons class="arrowdown" type="arrowdown" v-if="!changeArrow" @click="changeArrowClick"></uni-icons>
				<uni-icons class="arrowdown" type="arrowup" v-else="!changeArrow" @click="changeArrowClick" ></uni-icons>
			</view> -->
			<check-point :targetName="item.targetName"></check-point>
			<!-- <check-item 
			 ></check-item> -->
			<!-- <u-collapse :item-style="itemStyle" event-type="close" :arrow="arrow" :accordion="accordion" >
				<u-collapse-item :index="index" @change="changeArrowClick" :title="item.head" v-for="(item, index) in targetList" :key="index">
					<view class="collapse-item">
						{{item.targetName}}
					</view>
				</u-collapse-item>
			</u-collapse> -->
		</view>
		
	</view>
</template>

<script>
	import CheckPoint from './reCheckPoint'
	export default {
		components: {
			CheckPoint
		},
		data() {
			return {
				targetList: [{
					targetName: '温度'
				}],
				result: '',
				items: ['正常', '异常'],
				// 演示地址，请勿直接使用
				action: 'http://www.example.com/upload',
				fileList: [
					{
						url: 'http://pics.sc.chinaz.com/files/pic/pic9/201912/hpic1886.jpg',
					}
				],
				mark: '',
				type: 'textarea',
				border: true,
				height: 100,
				autoHeight: true,
				maxLength: 140,
				changeArrow: false
			}
		},
		computed: {
			
		},
		methods: {
			back() {
				this.$router.go(-1)
				console.log(11)
			},
			/**
			 * 完成
			 */
			finish() {
				
			},
			/**
			 * 折叠按钮箭头转换
			 */
			changeArrowClick() {
				this.changeArrow = !this.changeArrow
			}
		}
	}
</script>

<style lang="scss" scoped>
.nav-bar {
	background-color: #7aabc4;
}

/deep/ .uni-nav-bar-text[data-v-4afea59e] {
	font-weight: 600;
}

.wrapper {
	margin-bottom: 5px;
}

.header {
	line-height: 30px;
	height: 80px;
	font-size: 14px;
	background-color: white;
	border-bottom: 1px solid #ccc;
	.icon-left {
		display: inline-block;
		height: 20px;
		width: 7px;
		border-radius: 20px;
		background-color: #7AABC4;
		margin: 11px;
	}
	.text1 {
		color: #101010;
		font-size: 16px;
		font-weight: 600;
		margin-left: 10px;
		position: relative;
		bottom: -1px;
	}
	.tag {
		padding-left: 10px;
		img {
			height: 16px;
			width: 16px;
			margin-right: 10px;
		}
	}
	.arrowdown {
		position: absolute;
		right: 20px;
		top: 70px;
	}
}
.item-content {
	// height: 350px;
	background-color: white;
	padding-bottom: 15px;
	border-bottom: 1px solid #eee;
	.info {
		.uni-combox {
			display: inline-block;
			width: 80px;
			// border: 1px solid #ccc;
		}
		text {
			color: #7D7E80 100%;
			font-size: 16px;
			margin-left: 17px;
			color: #7D7E80;
		}
		input {
			border: 1px solid #ccc;
			display: inline-block;
			width: 80px;
			position: relative;
			top: 7px;
		}
	}
	.picture {
		text {
			color: #101010;
			font-size: 16px;
			font-weight: 600;
			margin: 15px;
		}
		.u-upload {
			margin: 10px;
		}
	}
	.mark {
		margin: 15px;
		text {
			color: #7D7E80;
			font-size: 16px;
			margin-bottom: 10px;
		}
		.tool {
			height: 15px;
		}
		textarea {
			border: 1px solid #ccc;
			margin: 15px;
			width: 685rpx;
		}
		.tips {
		  position: absolute;
		  margin-right: 15px;
		  right: 0;
		  font-weight: 400;
		  color: #7D7E80;
		}
	}
}
</style>
