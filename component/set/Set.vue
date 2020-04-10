<template>
	<view class="main">
		<view class="accounts">帐号管理</view>
		<view class="xmvip">
			<view class="xmvip-inner"  v-on:click="alter">
				<view class="txt">个人资料</view>
				<text> 〉</text>
			</view>
		</view>
		<view class="xmvip">
			<view class="xmvip-inner" v-on:click="site">
				<view class="txt">收货地址</view>
				<text> 〉</text>
			</view>
		</view>
		<view class="accounts">关于</view>
		<view class="xmvip">
			<view class="xmvip-inner">
				<view class="txt">关于商城</view>
				<text> 〉</text>
			</view>
		</view><view class="xmvip">
			<view class="xmvip-inner">
				<view class="txt">意见反馈</view>
				<text> 〉</text>
			</view>
		</view><view class="xmvip">
			<view class="xmvip-inner">
				<view class="txt">协议规则</view>
				<text> 〉</text>
			</view>
		</view><view class="xmvip">
			<view class="xmvip-inner">
				<view class="txt">资质证件</view>
				<text> 〉</text>
			</view>
		</view><view class="xmvip">
			<view class="xmvip-inner">
				<view class="txt">用户协议</view>
				<text> 〉</text>
			</view>
		</view><view class="xmvip">
			<view class="xmvip-inner">
				<view class="txt">隐私政策</view>
				<text> 〉</text>
			</view>
		</view>
		<view class="bottom">
			<view class="btn">退出登录</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			warp(){
				uni.navigateBack({
					delta:1
				})
			},
			site(){
				uni.navigateTo({
					url:'../place/Place'
				})
			},
			alter(){
				uni.navigateTo({
					url:'../../component/alter/Alter'
				})
			}
		}
	}
</script>

<style scoped>
	.main{color: #333333;font-size: 35upx;}
	.top{height: 150upx;line-height: 150upx;text-align: center;}
	.accounts{line-height: 90upx;background-color: #EEEEEE;padding-left: 30upx;color: #83878A;}
	.xmvip{line-height: 90upx;border-bottom: 2upx solid #F9F9F9;}
	.xmvip .txt{display: inline-block;margin-left: 25upx;width: 610upx;}
	.xmvip-inner{margin: 0 30upx;}
	.bottom{height: 250upx;background-color: #EEEEEE;padding-top: 50upx;}
	.btn{line-height: 100upx;width: 90%; margin:auto;text-align: center;background-color: #FFFFFF;border: 2upx solid #DEE1E5;}
	.pic image{width:35upx;height: 35upx;vertical-align: center;}
	.pic{display: inline-block;float: left;margin-left: 30upx;}
	.set{display: inline-block;}
</style>
