<template>
	<view class="main">
		<scroll-view class="main_box" scroll-y="true" @scrolltolower="lower">
			<view class="item" v-for="(item,index) in 5" :key="index">
				<view class="user">
					<image src="../../static/discovery/user.jpg" mode=""></image>
				</view>
				<view class="content">
					<view class="userName">
						来自务实家星球
					</view>
					<view class="img" v-if="index%2===0">
						<image src="../../static/discovery/user.jpg" mode="widthFix"></image>
						<image src="../../static/discovery/user.jpg" mode="widthFix"></image>
						<image src="../../static/discovery/user.jpg" mode="widthFix"></image>
						<image src="../../static/discovery/user.jpg" mode="widthFix"></image>
						<image src="../../static/discovery/user.jpg" mode="widthFix"></image>
						<image src="../../static/discovery/user.jpg" mode="widthFix"></image>
						<image src="../../static/discovery/user.jpg" mode="widthFix"></image>
						<image src="../../static/discovery/user.jpg" mode="widthFix"></image>
					</view>
					<video v-if="index%2!==0" src="../../static/w.mp4"  autoplay="true"></video>
					<view class="text">棕哥最帅</view>
					<view class="dsc">
						<view class="left">分享</view>
						<view class="love">爱心</view>
					</view>
				</view>

			</view>
		</scroll-view>
	</view>
</template>
<style lang="less" scoped>
	.main {
		background-image: linear-gradient(45deg, #0081ff, #1cbbb4);
	}

	// padding-bottom:120rpx;box-sizing: border-box;重要*************************保证页面底部内容不被隐藏也不会出现多余的滚动条
	.main_box {
		width: 100vw;
		height: 100vh;
		padding-bottom: 120rpx;
		box-sizing: border-box;
	}

	.main_centent {
		width: 100%;
		height: 100vh;
		color: #fff;
		letter-spacing: 4rpx;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	// image{width:750rpx;height: 750rpx;}
	.item {
		display: flex;
		// flex-direction: c;
		// padding: 0  0 0 15upx;
		background: #FFFFFF;

		.user {
			width: 150upx;
			height: 150upx;
			display: flex;
			align-items: center;
			justify-content: center;
			// flex: 1.5 0 0;

			image {
				width: 100upx;
				height: 100upx;
				border-radius: 50%;

			}
		}

		.content {
			margin: 20upx 0 0 0;

			// flex: 1;
			min-height: 400upx;
			// background: red;
			width: 100%;
			display: flex;
			flex-direction: column;

			.dsc {
				display: flex;
				justify-content: space-between;
				padding: 20upx;

			}

			.userName {
				color: #ccc;
				font-size: 24upx;
				padding: 10upx;
				font-weight: 400;
			}

			video {
				width: 300upx;
				height: 300upx;

			}
			.text{
				padding: 10upx;
				font-size: 28upx;
				color: #999999;
			}

			.img {
				// width: calc(100% - 20px);
				display: flex;
				flex-wrap: wrap;
				justify-content: start;

				image {
					border-radius: 40upx;
					padding: 4upx 10upx;
					height: 180upx;
					width: 180upx;

					// flex: 1;
					// width: 3;
				}
			}
		}
	}
</style>
<script>
	export default {
		data() {
			return {

			}
		},
		methods: {
			ontrueGetList() {
				uni.showToast({
					title: '第2个页面'
				})
				console.log("加载了第二个页面，可以把网络请求放这里")
			},
			lower() {
				uni.showToast({
					title: 'scroll-view的加载更多'
				})
				console.log("分页数据可以放这里~~~~~~嘿嘿")
			}
		}
	}
</script>
