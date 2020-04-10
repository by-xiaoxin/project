<template>
	<view class="message">
		<view class="message_content" v-for="(item,index) in information" :key="index">
			<view class="message_head">
				<view class="message_left">{{item.create_time}}</view>
				<view class="message_right">已发货</view>
			</view>
			<view class="message_centre" v-for="(item,index) in item.order_items" :key="index">
				<view class="message_image">
					<image :src="item.goods_item.cover"></image>
				</view>
				<view class="message_01">
					<view class="message_upa">{{item.goods_item.title}}</view>
					<view class="message_belowb">{{item.goods_skus.skus[0].value}} {{item.goods_skus.skus[1].value}}</view>
				</view>
				<view class="message_02">
					<view class="message_upc">{{item.price}}</view>
					<view class="message_belowd">x{{quantity}}</view>
				</view>
			</view>
			<view class="message_total">共3件商品，合计：￥299.00</view>
			<view class="message_trail">
				<view class="message_logistics">查看物流</view>
				<view class="message_affirm">确认收货</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				information: [],
				quantity:1
			}
		},
		onReady() {
			let _this = this
			uni.request({
				url: "http://ceshi3.dishait.cn/api/order/all",
				header: {
					token: '7dadcf0161710b5256265ed25cb7873b3fd61633'
				},
				method: 'POST',
				success(res) {
					_this.information = res.data.data
					console.log(res.data.data)
					for(let i=0;i<res.data.data.length;i++){
						for(let j=0;j<res.data.data[i].order_items.length;j++){
							let lopa=_this.information[i].order_items[j].goods_id
							let lopb=res.data.data[i].order_items[j].goods_id
							// let lopc=_this.information[i].order_items[0].goods_skus.skus[0].id
							// let lopd=res.data.data[i].order_items[0].goods_skus.skus[0].id
							// let lope=_this.information[i].order_items[0].goods_skus.skus[1].id
							// let lopf=res.data.data[i].order_items[0].goods_skus.skus[1].id
							// console.log(_this.information[i].order_items[j].goods_id)
							// console.log(res.data.data[i].order_items[j].goods_id)
							// if(lopa&&lopb){
							// 	console.log(lopa)
							// 	_this.quantity++;
								// return
							// }else{
							// 	_this.quantity=0						
							// }
							// if(lopa==25){
							// 	console.log(lopa)
							// 	console.log(lopb)
							// 	_this.quantity+=1
							// 	return
							// }
							
						}
					}
				}
			})
		}
	}
</script>

<style>
	.message {
		width: 100%;
		background-color: #F5F5F5;
		display: inline-block;
	}

	.message_content {
		width: 100%;
		background-color: #Fff;
		margin: 20upx 0upx;
	}

	.message_head {
		width: 100%;
		height: 80upx;
		line-height: 80upx;
		border-bottom: 2upx solid #F5F5F5;
	}

	.message_left {
		padding-left: 20upx;
		color: #BEBEBE;
		float: left;
		font-size: 30upx;
	}

	.message_right {
		padding-right: 25upx;
		color: #F66A08;
		float: right;
		font-size: 28upx;
	}

	.message_centre {
		width: 96%;
		height: 150upx;
		border-bottom: 2upx solid #F5F5F5;
		margin: auto;
		padding: 20upx 0upx;
	}

	.message_image {
		width: 20%;
		height: 150upx;
		float: left;
		padding: 0upx 20upx;
	}

	.message_image image {
		width: 100%;
		height: 150upx;
	}

	.message_01 {
		float: left;
		width: 50%;
		height: 150upx;
	}

	.message_upa {
		font-size: 33upx;
		padding-top: 23upx;
	}

	.message_belowb {
		font-size: 28upx;
		color: #B5B4AF;
		padding-top: 15upx;
	}

	.message_02 {
		float: left;
		width: 20%;
		height: 150upx;
	}

	.message_upc {
		width:100%;
		height:40rpx;
		float: right;
		padding-top: 22upx;
		font-size: 29upx;
		color: #B5B4AF;
		padding-bottom: 22upx;
		text-align:right;
	}

	.message_belowd {
		text-align:right;
		width:100%;
		height:30rpx;
		float: right;
		font-size: 28upx;
		color: #B5B4AF;
		line-height:30rpx;
	}	
	.message_total {
		font-size: 30upx;
		width: 100%;
		height: 80upx;
		line-height: 80upx;
		padding-left: 49%;
	}

	.message_trail {
		width: 100%;
		height: 90upx;
		line-height: 90upx;
	}

	.message_logistics {
		float: right;
		border: 1upx solid #E6E8EB;
		font-size: 28upx;
		text-align: center;
		width: 19%;
		height: 60upx;
		line-height: 60upx;
		color: #838A91;
		margin-right: 20upx;
	}

	.message_affirm {
		float: right;
		border: 1upx solid #E6E8EB;
		font-size: 28upx;
		text-align: center;
		width: 19%;
		height: 60upx;
		line-height: 60upx;
		color: #838A91;
		margin-right: 20upx;
	}
</style>
