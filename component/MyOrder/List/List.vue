<template>
	<view>
		<!-- 头部开始 -->
		<view class="titel_01">
			<view class="titel_02">
				<view class="box01">综合</view>
				<view class="box02">
					<view class="box03">
						<view class="box_01"></view>
					</view>
					<view class="box04">
						<view class="box_02"></view>
					</view>
				</view>
			</view>
			<view class="titel_02">
				<view class="box01">销量</view>
				<view class="box02">
					<view class="box03">
						<view class="box_01"></view>
					</view>
					<view class="box04">
						<view class="box_02"></view>
					</view>
				</view>
			</view>
			<view class="titel_02">
				<view class="box01">价格</view>
				<view class="box02">
					<view class="box03">
						<view class="box_01"></view>
					</view>
					<view class="box04">
						<view class="box_02"></view>
					</view>
				</view>
			</view>
			<view class="titel_02">筛选</view>
		</view>
		<!-- 头部结束 -->
		<!-- 内容开始 -->
		<view>
			<view class="content">
				<view class="box_left"><image src="https://tangzhe123-com.oss-cn-shenzhen.aliyuncs.com/public/5984928facd569ef906becba3469810b.png"></image></view>
				<view class="box_right">
					<view class="character_01">小米空调小米空</view>
					<view class="character_02">酒店格调 / 简约品味味 / 双雕方空味 / 新疆纯棉 / 新疆纯棉</view>
					<view class="character_03">￥120</view>
					<view class="character_04">1388微信开发者工具</view>
				</view>
			</view>
		</view>
		<!-- 内容结束 -->
	</view>
</template>

<script>
	export default {
		data() {
			return {

			}
		}
	}
</script>

<style>
	.titel_01 {
		width: 100%;
		height: 90upx;
		border-bottom: 1upx solid #F8F8F8;
		border-top: 1upx solid #F8F8F8;
	}

	.titel_02 {
		float: left;
		width: 25%;
		height: 100%;
		text-align: center;
		font-size: 30upx;
		line-height: 90upx;
		position: relative;
	}

	.box01 {
		width: 58%;
		float: left;
		height: 100%;
		text-align: right;
	}

	.box02 {
		width: 40%;
		float: left;
		height: 100%;
	}

	.box03 {
		width: 100%;
		float: left;
	}

	.box04 {
		width: 100%;
		float: left;
	}

	.box_01 {
		margin-top: 37upx;
		margin-left: 10upx;
		width: 0;
		height: 0;
		border-left: 10upx solid transparent;
		border-right: 10upx solid transparent;
		border-bottom: 10upx solid #B2B2B2;
	}

	.box_02 {
		margin-top: 5upx;
		margin-left: 10upx;
		width: 0;
		height: 0;
		border-left: 10upx solid transparent;
		border-right: 10upx solid transparent;
		border-top: 10upx solid #B2B2B2;
	}
	.content{
		width:100%;
		height:240upx;
		padding: 20upx 15upx;
		border-bottom: 1upx solid #F8F8F8;
	}
	.box_left{float:left;width:30%;height:100%;}
	.box_left image{width:100%;height:100%;border-radius:10upx;}
	.box_right{float:left;padding-left:30upx;width:55%;}
	.character_01{font-weight:900;font-size:35upx;padding-top:15upx;}
	.character_02{font-size:25upx;color:#7B838B;padding:8upx 0upx;}
	.character_03{color:#F7802C;font-weight:800;font-size:32upx;padding:8upx 0upx;}
	.character_04{font-size:23upx;color:#7B838B;padding:8upx 0upx;}
</style>
