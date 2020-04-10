<template>
	<view class="main">
		<view class="image">
			<view class="image-inner">
				<view class="txt">头像</view>
				<image class="pic" src="../../static/images/tx.jpg"></image>
			</view>
		</view>
		<view class="xmvip1">
			<view class="xmvip-inner">
				<view class="txt">姓名</view>
				<text>楚绵  〉</text>
			</view>
		</view>
		<view class="xmvip">
			<view class="xmvip-inner">
				<view class="txt">性别</view>
				<text> 〉</text>
			</view>
		</view>
		<view class="xmvip">
			<view class="xmvip-inner">
				<view class="txt">生日</view>
				<text> 〉</text>
			</view>
		</view>
		<view class="line"></view>
		<view class="xmvip">
			<view class="xmvip-inner">
				<view class="txt">修改密码</view>
				<text> 〉</text>
			</view>
		</view>
		<view class="xmvip">
			<view class="xmvip-inner">
				<view class="txt">密保手机</view>
				<text> 〉</text>
			</view>
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
			}
		}
	}
</script>

<style scoped>
	.main{color: #333333;font-size: 35upx;}
	.top{height: 150upx;line-height: 150upx;text-align: center;}
	.line{height: 20upx;background-color: #F5F5F5;}
	.image{line-height: 90upx;border-bottom: 2upx solid #F9F9F9;}
	.image .txt{display: inline-block;margin-left: 25upx;width: 540upx;}
	.image-inner{margin: 30upx 30upx;}
	.pic{display: inline-block;width: 120upx;height: 120upx;border-radius: 50%;vertical-align: middle;}
	.xmvip{line-height: 90upx;border-bottom: 2upx solid #F9F9F9;}
	.xmvip .txt{display: inline-block;margin-left: 25upx;width: 600upx;}
	.xmvip-inner{margin: 0 30upx;}
	.xmvip1{line-height: 90upx;border-bottom: 2upx solid #F9F9F9;}
	.xmvip1 .txt{display: inline-block;margin-left: 25upx;width: 525upx;}
	.pic1 image{width:35upx;height: 35upx;vertical-align: center;}
	.pic1{display: inline-block;float: left;margin-left: 30upx;margin-top: 20upx;}
	.modification{display: inline-block;}
</style>
