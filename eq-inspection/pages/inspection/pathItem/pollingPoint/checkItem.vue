<template>
	<view>
		<view class="item-content" v-show="foldStatus">
			<view class="info">
				<text class="text11">检查结果：</text>
				<uni-combox 
				:candidates="items" 
				v-model="result">
				</uni-combox>
				<text>数据信息：</text>
				<input type="text" :value="dataInfo" />
			</view>
			<view class="picture">
				<text>图片</text>
				<u-upload :action="action" :file-list="fileList" ></u-upload>
			</view>
			<view class="mark">
				<text>备注</text>
				<view class="tool" />
				<u-input v-model="mark" :type="type" :border="border" :height="height" :auto-height="autoHeight" :maxlength="maxLength" />
				<span class="tips">
					{{mark.length}}/{{maxLength}}
				</span>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: ['foldStatus'],
		data() {
			return {
				result: '',
				dataInfo: '',
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
		methods: {
			
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
		color: #7D7E80;
		font-size: 16px;
		// font-weight: 600;
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
			color: #7D7E80;
			font-size: 16px;
			
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
