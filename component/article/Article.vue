<template>
	<view class="main">
		<view class="top">
			<view class="pic" v-on:click="warp"><image src="../../static/images/left.png"></image>小米商城</view>
			<view class="cart"><image src="../../static/images/cart.png"></image></view>
		</view>
		<view style="padding:0 30upx;" class="text">
			<view class="title">Red mi K20 Pro常见购机咨询</view>
			<view class="title-inner">售前咨询:</view>
			<view>1.怎么参与Red mi K20 Pro订金预售</view>
			<view class="last">答:订金预售活动在5月28日18:00开启，成功支付订金后即表示成功预订Redmi K20 Pro手机。点
			击“我的”-“待付款”即可进行尾款支付，尾款支付时间为6月1日0点至24点。</view>
			<view>2.订金预售的订金可以退还吗?</view>
			<view class="last"> 答:支付100元订金后，可以申请退款，退款将在财务审核后及时退回。</view>
			<view> 3. Redmi K20 Pro标配什么充电器?</view>
			<view class="last">答:原装标配18W充电器。Redmi K20 Pro最高可支持27W有线快充，如有需要，可自行选购。</view>
			<view>4. Redmi K20 Pro有哪些套装可以购买?</view>
			<view>答:在售套装有:(1) Redmi K20 Pro+Redmi 20寸红色旅行箱套装。旅行箱原价299元，套装内价格199元</view>
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
		}
	}
</script>

<style scoped>
	.main{font-size: 34upx;}
	.top{height: 120upx;line-height: 120upx;border-bottom: 2upx solid #BEBEBE;position: fixed;}
	.top image{width: 40upx;height: 40upx;vertical-align: middle;margin-right: 30upx;}
	.cart{float: right;display: inline-block;}
	.pic{display: inline-block;}
	.text .title{font-size: 40upx;height: 120upx;line-height: 150upx;}
	.title-inner{font-size: 36upx;font-weight: 600;}
	.text view{line-height: 60upx;}
	.last{margin-bottom: 40upx;}
</style>
