<template>
	<view class="enter">
		<view class="topNev">
			<image src="../../../../static/enter/ooo.png" mode=""></image>
		</view>
		<view class="content">
			<text style="font-size: 55upx; font-weight: bold; line-height: 80upx; display: block;">手机号码登录</text>
			<view class="uni-form-item uni-column" style="line-height: 220upx; margin: 50upx 0; padding-bottom:20upx; border-bottom: #E1C6AB 2upx solid;">
				<input class="uni-input" type="number" @input="onaccount" placeholder="请输入手机号" />
			</view>
			<view class="uni-form-item uni-column" style="line-height: 220upx; margin: 50upx 0;">
				<input class="uni-input" style="width: 50%;" password type="text" @input="onpas" placeholder="请输入验证码" />
				<view class="ma" style="position: absolute; top: 424upx; right: 55upx; height: 100upx; line-height: 100upx; color: #838383;">
					获取验证码
				</view>
			</view>
			<view class="sj">
				用账号密码登录
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
				disabled:'true'
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
			btn: function() {
				let this_ =this
				if (this.account.length <= 0) {
					uni.showToast({
						icon: 'none',
						title: '请输入手机号'
					});
					return;
				}
				if (this.pas.length <= 0) {
					uni.showToast({
						icon: 'none',
						title: '请输入验证码'
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
						console.log(this_.account);
						console.log(this_.pas);
						console.log(res.data);
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
