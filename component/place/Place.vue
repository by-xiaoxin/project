<template>
	<view class="main">
		<view class="top">
			<view class="pic">
				<image src="../../static/images/left.png" @click="back"></image>
			</view>
			<view class="location">地址列表</view>
			<view class="add-address" v-on:click="add">
				<image class="add-img" src="../../static/images/add.png"></image>
			</view>
		</view>
		<scroll-view scroll-y style="height: 1200upx;">
			<view v-for="(item,index) in addressList" :key='index'>
				<view class="product-name-wrap" v-on:click="change(item,index)">
					<view class="list-item-info">{{item.name}}</view>
					<view style="display: inline-block;margin-left: 30upx;">{{item.phone}}</view> 
					<view class="list-item-address">
						{{item.province}}{{item.city}}{{item.district}}
					</view>
					<view class="right">
						<text> 〉</text>
					</view>
				</view>
			</view>
			</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				addressList:[]
			}
		},
		methods: {
			add(){
				uni.navigateTo({
					url:'../site/Site?type=add'
				})
			},
			change(item,index){
				let list = JSON.stringify(item)
				uni.navigateTo({
					url:'../site/Site?name='+list+'&type=change'
				})
			},
			back(){
				uni.navigateTo({
					url:'../../pages/personage/Personage'
				})
			}
		},
		onLoad: function(options){
			uni.showLoading({
			    title: '加载中'
			});
			var that = this
			uni.request({
				url:"http://ceshi3.dishait.cn/api/useraddresses/1",
				header:{
					"token":"a4c30e2a39426b875290fcbd91c16727b2b7e3c5"
				},
				success(res) {
					setTimeout(function () {
					    uni.hideLoading();
					}, 500);
					that.addressList = res.data.data
				}
			})
		},
		onShow() {
			this.onLoad();
		}
	}
</script>

<style scoped>
	.main{font-size: 32upx;}
	.top {height: 150upx;line-height: 150upx;text-align: center;width:100%;background-color: #F8F8F8;}
	.pic image {width: 35upx;height: 35upx;vertical-align: center;}
	.pic {display: inline-block;float: left;margin-left: 30upx;}
	.location {display: inline-block;}
	.product-name-wrap {margin: 20upx 30upx;font-size: 28upx;color: #404040;border-bottom: 2upx solid #f2f2f2;position: relative;}
	.list-item-info {margin: 10upx 0px; color:#E79556;display: inline-block;}
	.list-item-address {color: #585c64;margin-bottom: 20upx;}
	.right{position: absolute;top: 32%;right: 2%;}
	.add-address {display: inline-block;float: right;margin-right: 30upx;}
	.add-img {margin-right: 15upx;width: 35upx;height: 35upx;}
</style>
