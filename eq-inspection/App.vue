<script>
	export default {
		onLaunch: function() {
			console.log('App Launch');
		},
		onShow: function() {
			console.log('App Show');
		},
		onHide: function() {
			console.log('App Hide');
		}
	}
</script>

<style lang="scss">
	@import "uview-ui/index.scss";
/* 注意要写在第一行，同时给style标签加入lang="scss"属性 */
// @import "uview-ui/index.scss";
@import "static/css/color.scss";

	/*每个页面公共css */
	page {
		min-height: 100%;
		display: flex;
		.content {
			display: flex;
			flex: 1;
			flex-direction: column;
			background-color: $backgroudColor;
			.input-group {
				background-color: #ffffff;
				position: relative;
			}
			.input-group::before {
				position: absolute;
				right: 0;
				top: 0;
				left: 0;
				height: 0upx;
				content: '';
				-webkit-transform: scaleY(.5);
				transform: scaleY(.5);
				background-color: $lightColor;
			}
			.input-group::after {
				position: absolute;
				right: 0;
				bottom: 0;
				left: 0;
				height: 1px;
				content: '';
				-webkit-transform: scaleY(.5);
				transform: scaleY(.5);
				background-color:$lightColor;
			}
			.input-row {
				display: flex;
				flex-direction: row;
				position: relative;
				.title {
					width: 60px;
					height: 50upx;
					min-height: 50upx;
					padding: 15upx 0;
					padding-left: 30upx;
					line-height: 50upx;
				}
			}			
			.input-row.border::after {
				position: absolute;
				right: 0;
				bottom: 0;
				left: 15upx;
				height: 1upx;
				content: '';
				-webkit-transform: scaleY(.5);
				transform: scaleY(.5);
				background-color: $lightColor;
			}
			
			.btn-row {
				margin-top: 50upx;
				padding: 20upx;
			}
			
			button.primary {
				background-color: #0faeff;
			}
			/* 原生组件模式下需要注意组件外部样式 */
			m-input {
				width: 100%;
				min-height: 100%;
				display: flex;
			}
			uni-checkbox .uni-checkbox-input{
				height: 12px;
				width: 12px;
				color:#FFFFFF
			}
		}
	}

	/* #ifdef MP-BAIDU */
	page {
		width: 100%;
		height: 100%;
		display: block;
	}

	swan-template {
		width: 100%;
		min-height: 100%;
		display: flex;
	}

	/* 原生组件模式下需要注意组件外部样式 */
	custom-component {
		width: 100%;
		min-height: 100%;
		display: flex;
	}

	/* #endif */

	/* #ifdef MP-ALIPAY */
	page {
		min-height: 100vh;
	}

	/* #endif */
</style>
