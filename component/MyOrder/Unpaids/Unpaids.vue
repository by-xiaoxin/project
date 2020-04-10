<template>
	<view class="Unpaids">
		<view class="Unpaids_site">
			<view class="site_01">
				<view class="sites01">111111111</view>
				<view class="sites02">22222222222222</view>
			</view>
			<view class="site_02"><span class="box">></span></view>
		</view>
		<view class="Unpaids_quantity01">
			<view class="Unpaids_quantity02">
				<view class="Unpaids_image"><image src="https://tangzhe123-com.oss-cn-shenzhen.aliyuncs.com/public/5984928facd569ef906becba3469810b.png"></image></view>
				<view class="Unpaids_titel">共3件<span class="box">></span></view>
			</view>
		</view>
		<view class="Unpaids_total-prices">
			<view class="total-prices_left">商品总价</view>
			<view class="total-prices_right">￥20.00</view>
		</view>
		<view class="Unpaids_freight">
			<view class="freight_left">运费</view>
			<view class="freight_right">包邮</view>
		</view>
		<view class="Unpaids_discounts">
			<view class="discounts_left">优惠卷</view>
			<view class="discounts_right">无可用></view>
		</view>
		<view class="Unpaids_subtotal">
			<view class="subtotal_left">小计</view>
			<view class="subtotal_right">￥20.00</view>
		</view>
		<view class="Unpaids_invoice">
			<view class="invoice_left">发票</view>
			<view class="invoice_right" @click="invoice()">电子发票-{{boxtitel}}<span class="box">></span></view>
		</view>
		<view class="Unpaids_totals">
			<view class="atotals_left">合计：<span>￥20.00</span></view>
			<view class="atotals_right"><view class="total_bottom">去付款</view></view>
		</view>
	</view>
</template>

<script>
	let app = getApp();
	export default {
		data() {
			return {
				boxtitel:"",
			}
		},
		methods: {
			invoice() {
				console.log(app.globalData.box)
				wx.navigateTo({
					url:'../Lnvoice/Lnvoice'
				})
			}
		},
		onShow(){
			this.boxtitel=app.globalData.box
		}
	}
</script>

<style>
	.Unpaids{
		width:100%;
		background-color:#F5F5F5;
		display:inline-block;
	}
	.Unpaids_site{
		width:100%;
		height:300upx;
		background-color:#FD6801;
	}
	.site_01{
		float:left;
		width:75%;
		height:250upx;
		margin:25upx 0upx;
		margin-left:35upx;
		color:white;
	}
	.sites01{
		font-size:30upx;
		white:100%;
		height:60upx;
		margin-top:90upx;
		
	}
	.sites02{
		font-size:30upx;
		white:100%;
		height:60upx;
	}
	.site_02{
		float:right;
		width:20%;
		height:250upx;
		line-height:250upx;
		text-align:center;
		margin:25upx 0upx;
	}
	.Unpaids_quantity01{
		width:100%;
		height:130upx;
		background-color:#FD6801;
		border-bottom:2upx solid #F5F5F5;
	}
	.Unpaids_quantity02{
		width:100%;
		height:130upx;
		background-color:#fff;
		border-radius: 20upx 20upx 0upx 0upx;
		border-bottom:2upx solid #F5F5F5;
	}
	.Unpaids_image{
		width:50%;
		height:130upx;
		float:left;
	}
	.Unpaids_image image{
		width:25%;
		height:90upx;
		margin:20upx;
		margin-left:30upx;
	}
	.Unpaids_titel{
		width:20%;
		height:130upx;
		line-height:130upx;
		float:right;
		text-align: right;
		font-size:30upx;
		padding-right:30upx;
	}
	.Unpaids_invoice,.Unpaids_total-prices,.Unpaids_freight,.Unpaids_discounts,.Unpaids_subtotal{
		width:100%;
		height:80upx;
		background-color:#fff;
		border-bottom:2upx solid #F5F5F5;
		line-height:80upx;
		font-size:30upx;
	}
	.invoice_left,.subtotal_left,.total-prices_left,.freight_left,.discounts_left{
		float:left;
		padding-left:30upx;
	}
	.invoice_right,.subtotal_right,.total-prices_right,.freight_right,.discounts_right{
		float:right;
		padding-right:30upx;
	}
	.discounts_right{
		color:#CDCDCD;
		font-size:25upx;
	}
	.subtotal_left,.subtotal_right{
		color:#FD6801;
	}
	.Unpaids_invoice{
		margin-top:20upx;
		margin-bottom:220upx;
	}
	.Unpaids_totals{
		width:100%;
		height:80upx;
		background-color:#fff;
		position:fixed;
		bottom:0upx;
	}
	.atotals_left{
		float:left;
		width:72%;
		height:80upx;
		font-size:30upx;
		line-height:80upx;
		text-align:right;
	}
	.atotals_left span{
		color:#FD6801;
	}
	.atotals_right{
		float:right;
		display:inline-block;
		width:20%;
		height:80upx;
		margin:0upx 30upx;
	}
	.total_bottom{
		width: 100%;
		height: 55upx;
		background-color:#FD6801;
		color:white;
		font-size:28upx;
		line-height:55upx;
		text-align:center;
		border-radius:30upx;
		margin:12upx 0upx;
	}
	.box{
		color:#CDCDCD;
	}

</style>
