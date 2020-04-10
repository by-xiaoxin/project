<template>
	<view class="enter" :style="kcnueg !== true? 'display: none;':''">
		<view class="topNev">
			<image src="../../../../static/enter/ooo.png" mode="" @click="bianji"></image>
			<view class="top" style="float: right; margin-right: 30upx;color: #A7A7A7;">
				忘记密码
			</view>
		</view>
		<view class="content">
			<text style="font-size: 55upx; font-weight: bold; line-height: 80upx; display: block;">密码登录</text>
			<view class="uni-form-item uni-column" style="line-height: 220upx; margin: 50upx 0; padding-bottom:20upx; border-bottom: #E1C6AB 2upx solid;">
				<input class="uni-input" type="number" @input="onaccount" placeholder="请输入手机号/邮箱/小米账号" />
			</view>
			<view class="uni-form-item uni-column" style="line-height: 220upx; margin: 50upx 0;">
				<input class="uni-input" password type="text" @input="onpas" placeholder="请输入密码" />
			</view>
			<view class="sj" >
				用手机短信登录
				<image src="../../../../static/enter/jian.png" mode=""></image>
			</view>
			<view class="buttons">
				<button type="primary" @tap="btn" style="background-color: #F0AD4E;">登录</button>
			</view>
			<view class="checkbox">
				<label>
					<checkbox value="cb" color="#FFCC33" style="transform:scale(0.7)"  :checked="false" @click="checkBox(checked)" />
					<text style="margin-left:30upx ;">已经阅读并同意小米账号、隐私政策和小米商城用户协议</text>
				</label>
			</view>
			<view class="img">
				<image src="../../../../static/enter/jij.png" mode=""></image>
				<image src="../../../../static/enter/xinlan.png" mode=""></image>
			</view>
		</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				account:'',
				pas:'',
				checked:'',
				disabled:'true',
				miyao:'',
				kcnueg: true
			}
		},
		methods: {
			onaccount: function(event) {
				this.account = event.target.value
			},
			onpas: function(event) {
				this.pas = event.target.value
			},
			checkBox: function(a) { //是否禁用
				console.log(a)
				this.checked == a
				if (this.checked == "true") {
					this.disabled = false

				} else {
					this.disabled = true
				}


			},
			bianji(){//编辑按钮
				if(this.kcnueg == false){
					this.kcnueg = true
				}else{
					this.kcnueg = false
				}
			},
			btn: function() {
				let this_ =this
				if (this.account.length <= 0) {
					uni.showToast({
						icon: 'none',
						title: '请输入用户名'
					});
					return;
				}
				if (this.pas.length <= 0) {
					uni.showToast({
						icon: 'none',
						title: '请输入密码'
					});
					return;
				}
				uni.request({
					url: 'http://ceshi3.dishait.cn/api/login', //仅为示例，并非真实接口地址。
					data: {
						username:this_.account,//user2
						password:this_.pas//zcmcss
					},
					method: 'POST',
					success: (res) => {
						this_.miyao = res.data
						uni.setStorage({
						key:"miyao",
						data:res.data
						});
						console.log(this_.miyao)
							uni.showToast({
								icon: 'none',
								title: res.data.msg
							});
						if (res.data.msg == "ok") {
							uni.showToast({
							icon: 'none',
							title: '登录成功'
						});
							return;
						
						};
						
						
					},
					fail: () => {
						uni.showToast({
							icon: 'none',
							title: '网络异常,请稍后重试'
						});
					},
				})

			}

		},
		created() { //数据请求
			uni.getStorage({
			key:"miyao",
			success(e){
				console.log(e.data)
			e.data//这就是你想要取的token
			}
			});
		},



	}
</script>

<style scoped>
	.topNev {
		margin-top: 20upx;
		width: 100%;
		height: 100upx;
		line-height: 100upx;
		font-size: 35upx;
	}

	.topNev image {
		width: 80upx;
		height: 80upx;
	}

	.content {
		margin: 0 auto;
		margin-top: 80upx;
		width: 85%;
		height: 860upx;
	}

	.sj {
		font-size: 25upx;
		color: #A6A6A6;
	}

	.sj image {
		width: 25upx;
		height: 25upx;
	}

	.buttons {
		margin-top: 110upx;
		border-radius: 20upx;
		width: 100%;
		/* height: 110upx !important; */
		background-color: #FFD8B9;
		margin-bottom: 20upx;
	}

	.checkbox {
		font-size: 22upx;
		color: #C0C0C0;
	}

	.checkbox checkbox {
		width: 30upx;
		height: 30upx;
	}
	.img{
		margin-top: 100upx;
		margin-left: 35%;
	}
	.img image{
		margin-right: 20%;
		width: 35upx;
		height: 35upx;
	}
</style>
