<template>
	<view class="main">
		<view class="top_nav">
			<view class="user_image">
				<image src="../../static/discovery/user.jpg" mode=""></image>
			</view>
			<view class="user_message">
				<view class="top">
					<view class="left">彭凯</view>
					<view class="right">彭凯</view>
				</view>
				<view class="center">
					<view class="left">彭凯</view>
					<view class="right">彭凯</view>
				</view>
				<view class="bottom">
					<view class="left">彭凯</view>
					<view class="right">彭凯</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		data() {
			return{
				
			}
		},
		methods: {
	
		}
	}
</script>

<style lang="scss" scoped>
	.main{
		.top_nav{
			display: flex;
			background: red;
			width: 100vw;
			.user_image{
				image{
					width: 120upx;
					height: 120upx;
				}
			}
			.user_message{
				width: 100%;
				flex: 1;
				min-height: 120upx;
				background: red;
				.top{
					display: flex;
				}
			}
		}
		
		
	}
</style>