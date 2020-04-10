<template>
	<view class="main">
			<view class="top">
				<view class="pic" v-on:click="warp">
					<image src="../../static/images/left.png"></image>
				</view>
				<view class="compile">编辑收货地址</view>
				<view class="del" @click="del">删除</view>
			</view>
			<view class="xmvip">
				<view class="xmvip-inner">
					<view class="txt">收货人 : <input v-model="name" style="display: inline-block;overflow: initial;margin-left: 20upx;" />
					</view>
				</view>
			</view>
			<view class="xmvip">
				<view class="xmvip-inner">
					<view class="txt">手机号码 : <input v-model="phone" type="number" maxlength="11" style="display: inline-block;overflow: initial;margin-left: 20upx;" /></view>
				</view>
			</view>
			<view class="line"></view>
			<view class="xmvip">
				<view class="xmvip-inner">
					<view class="txt">所在地区 :
						<view class="tui-picker-content">
							<picker @change="changeRegin" mode="region" value="region">
								<view class="tui-picker-detail">{{region[0]}} - {{region[1]}} - {{region[2]}}</view>
							</picker>
						</view>
					</view>
				</view>
			</view>
			<view class="xmvip">
				<view class="xmvip-inner">
					<view class="txt">详细地址 : <input v-model="address" style="display: inline-block;overflow: initial;margin-left: 20upx;" /></view>
				</view>
			</view>
			<view class="line"></view>
			<view class="xmvip">
				<view class="xmvip-inner">
					<view class="txt">设为默认地址 : </view>
					<image class="pic1" @click="turn" :src="default1==1?'/static/images/on.png':'/static/images/off.png'"></image>
				</view>
			</view>
			<view class="bottom">
				<view class="bc" @click="save">保存</view>
			</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				region: ["广东省", "深圳市", "龙岗区"],
				name: '',//收货人
				phone: '',//电话
				address: '',//详细地址
				index: 0,//地址id
				default1: 1,//是否默认
				zip: "",//邮编
				type:''//修改还是新增
			}
		},
		methods: {
			//返回上一层
			warp() {
				uni.navigateBack({
					delta: 1
				})
			},
			//改变地址
			changeRegin(e) {
				this.region = e.target.value
			},
			//删除收货地址
			del() {
				let that = this
				uni.showModal({
					title: '提示',
					content: '是否确定删除？',
					success: function(res) {
						if (res.confirm) {
							uni.request({
								url: "http://ceshi3.dishait.cn/api/useraddresses/"+that.index+"",
								header: {
									"token": "a4c30e2a39426b875290fcbd91c16727b2b7e3c5"
								},
								method: "DELETE",
								success(res) {
									uni.navigateTo({
										url: '../place/Place?'
									})
								}
							})
						} else if (res.cancel) {
							alert('用户点击取消');
						}
					}
				});
			},
			//修改或新增收货地址
			save() {
				let that = this
				console.log(that.type)
				if(that.type=="change"&&that.region&&that.name&&that.phone&&that.address){
					uni.request({
						url: "http://ceshi3.dishait.cn/api/useraddresses/"+that.index+"",
						header: {
							"token": "a4c30e2a39426b875290fcbd91c16727b2b7e3c5"
						},
						method: "POST",
						data: {
							"province": that.region[0],
							"city": that.region[1],
							"district": that.region[2],
							"name": that.name,
							"phone": that.phone,
							'address': that.address,
							"default": that.default1,
							"zip": that.zip
						},
						success(res) {
							console.log(res)
							if (res.data.errorCode) {
								alert("信息填写不符合标准")
							} else {
								uni.navigateTo({
									url: '../place/Place'
								})
							}
						}
					})
				}else if(that.region&&that.name&&that.phone&&that.address){
					uni.request({
						url:'http://ceshi3.dishait.cn/api/useraddresses',
						header:{
							"token": "a4c30e2a39426b875290fcbd91c16727b2b7e3c5"
						},
						method:"POST",
						data: {
							"province": that.region[0],
							"city": that.region[1],
							"district": that.region[2],
							"name": that.name,
							"phone": that.phone,
							'address': that.address,
							"default": that.default1,
							"zip": that.zip
						},
						success(res){
							uni.navigateTo({
								url: '../place/Place'
							})
						}
					})
				}
			},
			//改变是否默认
			turn() {
				if (this.default1 == 0) {
					this.default1 = 1
				} else {
					this.default1 = 0
				}
			}
		},
		onLoad(option) {
			uni.showLoading({
				title: '加载中'
			});
			//初始化数据
			setTimeout(function() {
				uni.hideLoading();
			}, 500);
			let list = JSON.parse(option.name)
			this.region = [list.province, list.city, list.district]
			this.phone = list.phone
			this.name = list.name
			this.index = list.id
			this.type = option.type
		}
	}
</script>

<style scoped>
	.main {color: #333333;font-size: 35upx;}
	.top {height: 150upx;line-height: 150upx;text-align: center;background-color: #F8F8F8;}
	.xmvip {line-height: 90upx;border-bottom: 2upx solid #F9F9F9;}
	.xmvip .txt {margin-left: 25upx;color: #666;display: inline-block;}
	.xmvip-inner {margin: 0 30upx;}
	.line {height: 20upx;background-color: #F5F5F5;}
	.pic image {width: 35upx;height: 35upx;vertical-align: center;}
	.pic {display: inline-block;float: left;margin-left: 30upx;}
	.compile {display: inline-block;}
	.del {display: inline-block;float: right;color: #BEBEBE;margin-right: 30upx;}
	.pic1 {display: inline-block;width: 100upx;height: 60upx;float: right;margin-top: 20upx;}
	.bc {width: 80%;line-height: 80upx;margin: auto;background-color: #EC5151;text-align: center;color: #FFFFFF;}
	.bottom {padding-top: 50upx;}
	page {background-color: #efeff4;}
	.tui-picker-content {display: inline-block;}
	.tui-picker-name {height: 80upx;line-height: 80upx;}
	.tui-picker-detail {height: 80upx;line-height: 80upx;background-color: #fff;font-size: 35upx;padding: 0 10px;}
</style>
