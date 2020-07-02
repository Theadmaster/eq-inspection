<template>
	<view class="content">
		<view class="list-items">
			<view class="item">
				<view class="route heng">
					<view class="left">
						<img src="../../static/img/user.png" alt="">
						<view>路线21</view>
					</view>
					<view class="right">
						<img src="../../static/img/working.png" alt="">
						<view>进行中</view>
					</view>
				</view>
				<view class="circle heng">
					<img src="../../static/img/circle.png" alt="">
					<view>循环周期：每周一次</view>
				</view>
				<view class="start-date heng">
					<img src="../../static/img/starttime.png" alt="">
					<view>开始时间：2020/04/09 13:30:25</view>
				</view>
				<view class="point" @click="open">
					<i></i><i></i><i></i>
				</view>
			</view>
		</view>
		<view>
			<uni-popuo ref="popup"  type="buttom">底部弹出</uni-popuo>
		</view>
	</view>
</template>

<script>
	import uniPopup from '../../components/uni-popup/uni-popup.vue'
	export default {
		data() {
			return {
				
			};
		},
		components: uniPopup,
		
		methods:{
			open(){
			  this.$refs.popup.open()
			}
		}
	}
</script>

<style lang="scss">
.content{
	.list-items{
		.item{
			background: #ffffff;
			padding: 10px 20px;
			font-size: 16px;
			position: relative;
			.heng{
				display: flex;
				align-items: center;
				img{
					width: 20px;
					height: 20px;
				}
				view{
					display: inline-block;
					padding:5px 2px;
				}
			}
			.route{
				display: flex;
				
				
				.left{
					flex: 1;
				}
				.right{
					display: flex;
					align-items: center;
					img{
						width: 15px;
						height: 15px;
					}
				}
			}
			.point{
				position: absolute;
				bottom: 15px;
				right: 20px;
				i{
					display:block; 
					width:3px; 
					height:3px; 
					background-color:rgb(128, 129, 130); 
					margin:3px; 
					border-radius:50%
				}
			}
		}
	}
}
</style>
