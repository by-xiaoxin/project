<template>
	<view class="main">
		<!-- 上部分 -->
		<view class="top">
			<image src="../../static/images/bg.jpg" class="bg-img" ></image>
			<view class="tx" >
				<image class="tx-img" src="../../static/images/tx.jpg"></image>
				<view style="display: inline-block;width: 150upx;margin-left: 20upx;color: #FFFFFF;">测试昵称</view>
			</view>
			<image src="../../static/images/info.png" class="xx"></image>
			<view class="vip">
				<image class="vip-img" src="../../static/images/crown(1).png"></image>
				<view style="display: inline-block;margin-left: 10upx;color: #F4EB36;">会员积分 1.99</view>
			</view>
		</view>
		<!-- 中间状态部分 -->
		<view class="midder">
			<view class="docu">
				<view class="left">我的订单</view>
				<view class="right" @click="dd">全部订单 〉</view>
			</view>
			<view class="zt">
				<view class="df">
					<image src="../../static/images/payment.png"></image>
					<view>待付款</view>
				</view>
				<view class="df">
					<image src="../../static/images/receiving.png"></image>
					<view>待收货</view>
				</view>
				<view class="df">
					<image src="../../static/images/remain.png"></image>
					<view>待评价</view>
				</view>
				<view class="df">
					<image src="../../static/images/maintain.png"></image>
					<view>退换修</view>
				</view>
			</view>
			<view  class="line"></view>
			<view class="line-img"><image src="../../static/images/bg.png"></image></view>
		</view>
		<view class="bottom">
			<view class="xmvip">
				<view class="xmvip-inner">
					<image src="../../static/images/VIP.png"></image>
					<view class="txt">小米会员</view>
					<text> 〉</text>
				</view>
			</view>
			<view class="xmvip">
				<view class="xmvip-inner">
					<image src="../../static/images/crown(1).png"></image>
					<view class="txt">会员中心</view>
					<text> 〉</text>
				</view>
			</view>
			<view class="xmvip">
				<view class="xmvip-inner">
					<image src="../../static/images/heat.png"></image>
					<view class="txt">服务中心</view>
					<text> 〉</text>
				</view>
			</view>
			<view class="xmvip">
				<view class="xmvip-inner">
					<image src="../../static/images/horse.png"></image>
					<view class="txt">小米之家</view>
					<text> 〉</text>
				</view>
			</view>
			<view class="xmvip">
				<view class="xmvip-inner">
					<image src="../../static/images/grass.png"></image>
					<view class="txt">更多功能</view>
					<text> 〉</text>
				</view>
			</view>
			<view  class="line"></view>
			<view class="xmvip">
				<view class="xmvip-inner" v-on:click="set">
					<image src="../../static/images/set.png"></image>
					<view class="txt">更多设置</view>
					<text> 〉</text>
				</view>
			</view>	
		</view>
	</view>
</template>

<script>
	export default {
		data(){
			return{
				statusBarHeight:''
			}
		},
		methods:{
			set(){
				uni.navigateTo({
					url:'../../component/set/Set'
				})
			},
			dd(){
				uni.navigateTo({
					url:'../../component/MyOrder/Subject/Subject'
				})
			}
		},
		onLoad() {
			var that = this
			uni.getSystemInfo({
			    success(res) {
					that.statusBarHeight = res.statusBarHeight
			    }
			})
		},
	}
</script>

<style scoped>
	.main{font-size: 32upx;color: #333333;}
	/* 上半部分 */
	.top{width: 100%;height: 340upx;position: relative;}
	.top .bg-img{width: 100%;height: 340upx;}
	.tx{position: absolute;top: 120upx;left: 60upx;}
	.tx .tx-img{width: 120upx;height: 120upx;border-radius: 50%;display: inline-block;vertical-align: middle;}
	.xx{position: absolute;top: 50upx;right: 50upx;width: 50upx;height: 50upx;}
	.vip{width: 300upx;position: absolute;right: 0;bottom: 70upx;background-color: #FCAD01;line-height: 70upx;text-align: center; border-radius: 50upx 0 0 50upx;}
	.vip .vip-img{width: 60upx;height: 60upx;display: inline-block;vertical-align: middle;margin-bottom: 13upx;}
	/* 中间状态部分 */
	.docu{line-height: 80upx;border-bottom: 4upx solid #F7F7F7;margin: 0 20upx;height: 80upx;}
	.docu .left{float: left;font-size: 36upx;}
	.docu .right{float: right;color: #778086;}
	.zt{display: flex;justify-content: space-between;height: 130upx;margin: 20upx 50upx 0 50upx;}
	.zt image{width: 70upx;height: 70upx;vertical-align: middle;margin-left: 10upx;}
	.line{height: 20upx;background-color: #F5F5F5;}
	.line-img image{height: 280upx;width: 100%;}
	/* 底部 */
	.xmvip{line-height: 90upx;border-bottom: 2upx solid #F9F9F9;}
	.xmvip image{width: 40upx;height: 40upx;display: inline-block;vertical-align: middle;}
	.xmvip .txt{display: inline-block;margin-left: 30upx;width: 580upx;}
	.xmvip-inner{margin: 0 30upx;}
</style>
