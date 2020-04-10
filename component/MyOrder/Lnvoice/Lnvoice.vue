<template>
	<view class="Lnvoice">
		<view class="Lnvoice_01">
			<view class="Lnvoice_type">发票类型</view>
			<view class="Lnvoice_buttom">电子发票</view>
			<view class="Lnvoice_title">
				电子发票与纸质发票具有相同的法律效力，可作为报销、售后、
				维权凭证，推荐使用电子发票，不怕丢失，更方便，环保。
			</view>
		</view>
		<view class="Lnvoice_02">
			<view class="Lnvoice_rise">发票抬头</view>
			<view class="Lnvoice_type02">
				<view :class="['Lnvoice_unit',index==boxindex ? 'Lnvoice_personage':'']" v-for="(item,index) in contentq" :key="index" @click="show(index)">{{item}}</view>
			</view>
		</view>
		<view class="Lnvoice_03">
			<view class="Lnvoice_name">个人姓名：个人</view>
			<view class="Lnvoice_content">发票内容：商品明细</view>
		</view>
		<view class="Lnvoice_04">收票人手机：158****1215</view>
		<view class="Lnvoice_05">
			<view class="Lnvoice_character01">发票须知：</view>
			<view class="Lnvoice_character02">1.发票位实现支付金额，不包括优惠卷等；</view>
			<view class="Lnvoice_character03">2.电子发票可在订单完成后，在订单详情中查看；</view>
		</view>
	</view>
</template>

<script>
	let app = getApp();
	export default {
		data() {
			return {
				contentq:["个人","单位"],
				boxindex:0,
			}
		},
		methods:{
			show(e){
				this.boxindex=e
				if(e==0){
					app.globalData.box=this.contentq[0]
				}else{
					app.globalData.box=this.contentq[1]
				}
			}
		}
	}
</script>

<style>
	.Lnvoice{
		width:100%;
		background-color:#F5F5F5;
		display:inline-block;
	}
	.Lnvoice_01{
		width:100%;
		height:275upx;
		background-color:#fff;
		margin:20upx 0upx;
		padding:20upx 0upx;
	}
	.Lnvoice_type{
		width:100%;
		height:60upx;
		line-height:60upx;
		font-size:30upx;
		padding-left:20upx;
	}
	.Lnvoice_buttom{
		width:170upx;
		height:55upx;
		line-height:55upx;
		margin-left:20upx;
		background-color:#FBE0D4;
		border:1upx solid #F39552;
		color:#F39552;
		text-align: center;
		font-size:26upx;
		margin-top:20upx;
	}
	.Lnvoice_title{
		width:96%;
		height:120upx;
		color:#CACACA;
		font-size:28upx;
		padding-left:20upx;
		margin-top:25upx;
	}
	.Lnvoice_02{
		width:100%;
		height:190upx;
		margin-bottom:20upx;
		background-color:#fff;
	}
	.Lnvoice_rise{
		width:100%;
		height:80upx;
		line-height:80upx;
		font-size:30upx;
		padding-left:20upx;
	}
	.Lnvoice_type02{
		width:100%;
		height:100upx;
		line-height:100upx;
	}
	.Lnvoice_personage{
		background-color:#FBE0D4!important;
		border:1upx solid #F39552;
		color:#F39552;
	}
	.Lnvoice_unit{
		float:left;
		width:170upx;
		height:55upx;
		line-height:55upx;
		margin-left:20upx;
		background-color:#F8F9FB;
		text-align: center;
		font-size:26upx;
		margin:20upx 20upx;
	}
	.Lnvoice_03{
		width:100%;
		height:180upx;
		background-color:#fff;
		margin-bottom:20upx;
	}
	.Lnvoice_name{
		font-size:30upx;
		width:100%;
		height:90upx;
		line-height:90upx;
		padding-left:20upx;
		border-bottom:1upx solid #E8E9ED;
	}
	.Lnvoice_content{
		font-size:30upx;
		width:100%;
		height:90upx;
		line-height:90upx;
		padding-left:20upx;
	}
	.Lnvoice_04{
		width:100%;
		height:80upx;
		font-size:30upx;
		line-height:80upx;
		padding-left:20upx;
		margin-bottom:20upx;
		background-color:#fff;
	}
	.Lnvoice_05{
		width:100%;
		height:220upx;
		font-size:28upx;
		color:#BDBDBD;
	}
	.Lnvoice_character01{
		padding-left:20upx;
	}
	.Lnvoice_character02{
		padding-left:20upx;
		line-height:80upx;
	}
	.Lnvoice_character03{
		padding-left:20upx;
		line-height:20upx;
	}
</style>
