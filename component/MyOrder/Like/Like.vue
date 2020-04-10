<template>
	<view>
		<view class="coffee">
			<view class="like_s">猜你喜欢</view>
			<view class="like_a">————————&nbsp;&nbsp;&nbsp;实时推荐你的爱&nbsp;&nbsp;&nbsp;————————</view>
			<view class="like_z" v-for="item in bocxget" :key="index">
				<view class="like_image"><image :src="item.cover"></image></view>
				<view class="like_titel01">{{item.title}}</view>
				<view class="like_titel02">1.5匹支流变频</view>
				<view class="like_titel03">
					<view class="like_big">￥{{item.min_price}}</view>
					<view class="like_little">￥{{item.min_oprice}}</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {	
				bocxget:[]
			}
		},
		onReady(){
			let _this=this
			uni.request({
				url: "http://ceshi3.dishait.cn/api/goods/hotlist",
				success(res) {
					_this.bocxget = res.data.data
				}
			})
		}
	}
</script>

<style>
	.coffee{
		width:100%;
		background-color:#F5F5F5;
		display:inline-block;
	}
	.like_s {
		width: 100%;
		height: 50upx;
		line-height: 50upx;
		text-align: center;
		font-weight: bold;
		font-size:35upx;
		color:#F96B08;
		margin-top:60upx;
	}
	.like_a{
		width:100%;
		height: 40upx;
		line-height: 40upx;
		font-size:28.1upx;
		text-align: center;
		color:#B8B8B8;
	}
	.like_z{
		width:47%;
		height:500upx;
		float:left;
		background-color:#fff;
		margin:25upx 0upx;
		margin-left:2%;
	}
	.like_image image{
		width:100%;
		height:350upx;
	}
	.like_titel01{
		font-size:30upx;
		line-height: 40upx;
		padding-left:20upx;
	}
	.like_titel02{
		font-size:23upx;
		color:#626669;
		padding-left:20upx;
		line-height: 40upx;
	}
	.like_titel03{
		padding-left:20upx;
		padding-top:4upx;
	}
	.like_titel03 .like_big{
		color:red;
		font-size:28upx;
		float:left;
		padding-right:10upx;
	}
	.like_titel03 .like_little{
		color:#626669;
		font-size:20upx;
		text-decoration:line-through;
		padding-top:11upx;
	}
</style>
