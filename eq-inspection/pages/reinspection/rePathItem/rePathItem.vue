<template>
	<view class="content">
		<!-- 顶部导航栏 -->
		<uni-nav-bar 
		background-color="#7aabc4"
		color="white"
		left-icon="back"
		title="路线21"
		@clickRight="filtrate"
		@clickLeft="back"
		>
			<view slot="right">
				<img class="img-right" src="../../../static/img/scan.png" />
				<img class="img-right" src="../../../static/img/select.png" />
			</view>
		</uni-nav-bar>
		
		<!-- 占位工具人一号 -->
		<view class="placehoder" />
		
		<!-- 任务列表 -->
		<view v-for="(item,index) in taskList" :key="index" class="card">
			<view class="card-head">
				<icon class="icon-left" type="" />
				<text class="text1">{{item.pathName}}</text>
				<img v-if="item.status === 2" src="../../../static/img/working.png" alt=""></img>
				<img v-else-if="item.status === 1" src="../../../static/img/waitfinish.png" alt=""></img>
				<img v-else="item.status === 3" src="../../../static/img/finished.png" alt=""></img>
				<text class="text2">{{item.statusValue}}</text>
			</view>
			
			<view class="period card-content">
				<img src="../../../static/img/count.png" class="img1" />
				<text>完成指标数: {{item.count}}</text>
			</view>
			<view class="begin card-content">
				<img src="../../../static/img/category.png" />
				<text>设备类别: {{item.category}}</text>
			</view>
			<img src="../../../static/img/more.png" alt="" class="more" @click="moreClick(item)" />
		</view>
		
		<!-- 占位工具人二号 -->
		<view class="placehoder2" />
		
		<!-- 暂无更多任务 -->
		<view class="info">
			<text>————暂无更多任务————</text>
		</view>
		
		<!-- 弹出框 -->
		<uni-popup ref="popup" type="bottom">
			<view class="dialog">
				<view class="item" v-if="showFinish" @click="finishTaskClick">
					完成巡检
				</view>
				<view class="item item2" @click="checkTaskClick">
					查看巡检项
				</view>
				<view class="item item3" @click="cancelClick">
					取消
				</view>
			</view>
		</uni-popup>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				taskList: [{
					id: 1,
					pathName: '巡检点01',
					count: '2/28',
					category: '压强',
					status: 2,
					statusValue: '进行中',
				},{
					id: 2,
					pathName: '巡检点02',
					count: '2/28',
					category: '压强',
					status: 1,
					statusValue: '待巡检'
				},{
					id: 3,
					pathName: '巡检点03',
					count: '28/28',
					category: '压强',
					status: 3,
					statusValue: '已完成'
				}],
				showFinish: true,
				currentItem: null
			};
		},
		methods: {
			back() {
				this.$router.go(-1)
			},
			/**
			 * 筛选
			 */
			filtrate() {
				console.log('123')
			},
			moreClick(item) {
				this.currentItem = item
				/**
				 * 如果已完成或者该路线负责人不是当前用户则不显示完成任务
				 */
				if(item.status === 3) {
					this.showFinish = false
				}else {
					this.showFinish = true
				}
				this.$refs.popup.open()
			},
			/**
			 * 查看巡检
			 */
			checkTaskClick() {
				uni.navigateTo({
					url:'./rePollingPoint/rePollingPoint'
				})
				this.$refs.popup.close()
			},
			/**
			 * 取消任务
			 */
			cancelClick() {
				this.$refs.popup.close()
			},
			/**
			 * 完成任务
			 */
			finishTaskClick() {
				this.$refs.popup.close()
			}
		}
	}
</script>

<style lang="scss">
.nav-bar {
	background-color: #7aabc4;
}

/deep/ .uni-nav-bar-text[data-v-4afea59e] {
	font-weight: 600;
}

.img-right {
	position: relative;
	top: 8px;
	margin-left: 10px;
}
	
.placehoder {
	height: 5px;
}

.card {
	background-color: white;
	height: 100px;
	padding-left: 20px;
	margin-bottom: 5px;
	.card-head {
		display: flex;
		align-items: center;
		height: 40px;
		font-size: 14px;
		.icon-left {
			display: inline-block;
			height: 20px;
			width: 7px;
			border-radius: 20px;
			background-color: #7AABC4;
			margin: 11px;
		}
		img {
			height: 20px;
			width: 20px;
			position: absolute;
			right: 60px;
		}
		.text1 {
			color: #101010;
			font-size: 16px;
			font-weight: 600;
		}
		.text2 {
			position: absolute;
			right: 12px;
			font-size: 14px;
			color: #7D7E80;
		}
	}
	.card-content {
		margin-left: 10px;
		display: flex;
		align-items: center;
		img {
			height: 25px;
			width: 25px;
			margin-right: 5px;
		}
		
		text {
			font-size: 14px;
		}
		
	}
	.more {
		position: relative;
		left: 310px;
		top: -27px;
		height: 24px;
		width: 24px;
	}
}

.placehoder2 {
	height: 180px;
}

.info {
	text-align: center;
	font-size: 14px;
	color: #101010;
}

.dialog {
	
	background-color: white;
	border-top-right-radius: 20px;
	border-top-left-radius: 20px;
	.item {
		height: 70px;
		text-align: center;
		line-height: 70px;
		font-size: 15px;
		font-weight: 600;
		border-bottom: 1px solid #eee;
	}
	.item2 {
		border-bottom: 2px solid #ccc !important;
	}
	.item3 {
		font-weight: 500 !important;
	}
}
</style>
