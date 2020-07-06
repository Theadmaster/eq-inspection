<template>
	<view>
		<view class="header">
			<icon class="icon-left" type="" />
			<text class="text1">{{targetName}}</text>
			<view class="tag">
				<img src="../../../../static/img/tag.png"  />
				<text>当前状态：待巡检</text>
			</view>
			<uni-icons class="arrowdown" type="arrowdown" v-if="!changeArrow" @click="changeArrowClick"></uni-icons>
			<uni-icons class="arrowdown" type="arrowup" v-else="!changeArrow" @click="changeArrowClick" ></uni-icons>
		</view>
		<check-item :foldStatus="changeArrow"></check-item>
	</view>
</template>

<script>
	import CheckItem from './checkItem'
	export default {
		components: {
			CheckItem
		},
		props: ['targetName'],
		data() {
			return {
				changeArrow: false
			}
		},
		methods: {
			/**
			 * 折叠按钮箭头转换
			 */
			changeArrowClick() {
				console.log(111)
				this.changeArrow = !this.changeArrow
			}
		}
	}
</script>

<style lang="scss" scoped>
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
</style>
