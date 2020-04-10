<template>
	<view class="title">
		<view class="title_1">为你推荐</view>
		<view class="title_2">---------------- 买了人还买 ----------------</view>
		<view class="con">
			<view class="conbox"  v-for="(item,index) in img" :key="index">
				<view class="imag">
					<image :src="item.cover" mode=""></image>
				</view>
				<view class="t1">
					{{item.title}}
				</view>
				<view class="t2">
					1.5匹支流变频
				</view>
				<view class="t3">
					<text>￥{{item.min_price}}</text><text style="display: inline-block; margin-left: 20upx; font-size: 25upx; color: #8A9095;text-decoration:line-through">￥{{item.min_oprice}}</text>
				</view>
			</view>
		</view>
	</view>

</template>

<script>
	export default {
		data() {
			return {
				img:'',
				guli: '',
			}
		},
		methods: {

		},
		created() { //数据请求
			let this_ = this
			uni.request({
				url: 'http://ceshi3.dishait.cn/api/goods/hotlist', //接口地址。
				// data: {
				//     name: 'name'
				// },
				// header: {
				//     'custom-header': 'hello' //自定义请求头信息
				// },
				success(res) {

					this_.img = res.data.data
					console.log(this_.img)
				}
			});
		}
	}
</script>

<style scoped>


	.title_1 {
		text-align: center;
		font-weight: bold;
		color: #F86A06;
		font-size: 35upx;
		line-height: 100upx;
	}

	.title_2 {
		text-align: center;
		color: #C4C4C4;
		font-size: 35upx;
		line-height: 50upx;
	}
.con{
	width: 100%;
	height: 1400upx;
	clear: both;
	margin-bottom: 50upx;
}
	.conbox {
		margin-top: 20upx;
		width: 50%;
		height: 410upx;
		float: left;
	}
	.imag{
		margin-left: 45upx;
	}
	.conbox image{
		width: 250upx;
		height: 250upx;
	}
	.t1{
		padding-left:15upx ;
		margin-top: 20upx;
		font-size: 30upx;
	}
	.t2{
		padding-left:15upx ;
		font-size: 25upx;
		color: #8A9095;
	}
	.t3{
		padding-left:15upx ;
		font-size: 25upx;
		color: #D83647;
		margin-bottom: 25upx;
	}
</style>
