<template>
	<view class="content">
		<button class="Btn" type='primary'  size="mini" open-type="getUserInfo"  withCredentials="true" lang="zh_CN" @getuserinfo="auth" >授权登录</button>
		<!-- 比赛 -->
		<tab-game :style="{'display':show_index == 0 ?'block':'none'}" ref="game"></tab-game>
		<!-- 发现 -->
		<tab-discovery :style="{'display':show_index == 1 ?'flex':'none'}" ref="discovery"></tab-discovery>
		<!-- 数据 -->
		<tab-data :style="{'display':show_index == 2? 'block':'none'}"  ref="data"></tab-data>
		<!-- 资讯 -->
		<tab-information :style="{'display':show_index == 3 ?'block':'none'}" ref="information"></tab-information>
		<!-- 个人中心 -->
		<tab-mycenter :style="{'display':show_index == 4 ? 'flex':'none'}" ref="mycenter"></tab-mycenter>
		<!-- is_lhp判断是否为刘海屏在main.js里，好像uniapp有一个css变量获取刘海屏的安全区域 -->
		<view class="tabBar" :style="{height:is_lhp?'140rpx':'98rpx'}">
			<!-- 导航的中间圆圈 --> 
			<view class="border_box" :style="{paddingBottom:is_lhp?'40rpx':''}">
				<view class="tabBar_miden_border"></view>
			</view>
			<view class="tabBar_list" :style="{paddingBottom:is_lhp?'40rpx':''}">
				<view v-for="(item) in tab_nav_list" :key="item.id" :class="{'tabBar_item':item.id!=2,'tabBar_item2':item.id==2}" @tap="cut_index(item.id)">
					<image v-if="show_index == item.id"  :src="`../../static/tabBar/${item.id+1}${item.id+1}.png`"></image>
					<image v-else :src="`../../static/tabBar/${item.id+1}.png`"></image>
					<view :class="{'tabBar_name':true,'nav_active':show_index == item.id}">{{item.name}}</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import tabGame from '@/components/tabBar/game.vue'
	import tabDiscovery from '@/components/tabBar/discovery.vue'
	import tabInformation from '@/components/tabBar/information.vue'
	import tabData from '@/components/tabBar/Data.vue'
	import tabMycenter from '@/components/tabBar/mycenter.vue'
	export default {
		components: {
			tabGame,//比赛    0
			tabDiscovery,//发现    1
			tabInformation,//资讯   2
			tabData,//数据   3
			tabMycenter//个人中心  4
		},
		data() {
			return {
				show_index:4,//控制显示那个组件
				tab_nav_list :[{'id':0,'name':'首页'},{'id':1,'name':'动态'},{'id':2,'name':'发布瞬间'},{'id':3,'name':'关注'},{'id':4,'name':'我的'}],//菜单列表
				is_lhp:false
			}
		},
		onLoad() {
			this.is_lhp = this.$is_bang
			this.$nextTick(function(){
				// 一定要等视图更新完再调用方法   -----------++++++++++++++++重要
				this.$refs.game.ontrueGetList()//初次加载第一个页面的请求数据
			})
			
			console.log("是否为刘海屏",this.is_lhp ) 
		},
		methods: {
			auth(){
				uni.login({
					success(res) {
						console.log(res)
						uni.getUserInfo({
						      provider: 'weixin',
						      success: function (infoRes) {
						        console.log( infoRes);
						      }
						    });
					}
				})
				
			},
			// 切换组件
			cut_index(type){
				console.log('----------------------------------',type)
				this.show_index = type
				if(this.show_index == 0){
					this.$refs.game.ontrueGetList()
				}
				else if(this.show_index == 1){
					this.$refs.discovery.ontrueGetList()
				}
				else if(this.show_index == 2){
					this.$refs.data.ontrueGetList()
				}
				else if(this.show_index == 3){
					this.$refs.information.ontrueGetList()
				}
				else if(this.show_index == 4){
					// this.$refs.mycenter.ontrueGetList()
				}
			},
			onPullDownRefresh(){
				uni.showToast({
					title:`第${this.show_index+1}个页面的刷新`
				})
				setTimeout(function(){
					uni.stopPullDownRefresh()
				},2000)
				console.log('下拉刷新四个组件公用的下拉刷新方法,根据在哪个页面下拉执行哪个页面的刷新方方法即可')
				console.log('如果想要自定义刷新的话，插件市场就有一个   非常好用也非常容易入手')
			}
		}
	}
</script>

<style lang="scss" scoped>
	.tabBar{ width:100%;height: 98rpx;background: #fff;border-top:1px solid #E5E5E5;position: fixed;bottom:0px;left:0px;right:0px;display: flex;align-items: center;justify-content: center;
		.tabBar_list{ width:86%;display: flex;justify-content: space-between;
			image{ width:48rpx;height: 48rpx;margin-bottom:2rpx}
			.tabBar_item{ width:68rpx;display: flex;justify-content: center;align-items: center;flex-direction: column;font-size: 20rpx;color: #969BA3;}
			.tabBar_item2{
				width:100rpx;height:100%;display: flex;justify-content: center;align-items: center;flex-direction: column;font-size: 20rpx;color: #969BA3;margin-top:-20rpx;position: relative;z-index: 101;
				image{ width:68rpx;height: 68rpx;}
			}
		 } 
	}
	.border_box{
		// pointer-events: none; 事件穿透解决z-index层级问题
		width:100%;height: 100rpx;display: flex;justify-content: center;align-items: center;position: fixed;left:0px;bottom:50rpx;z-index: 100;pointer-events: none;
		.tabBar_miden_border{   width:100rpx;height:50rpx;border-top:2rpx solid #E5E5E5;border-radius:50rpx 50rpx 0 0; /* 左上、右上、右下、左下 */background: #fff;}
	}
	.nav_active{color: #007AFF;}
</style>
