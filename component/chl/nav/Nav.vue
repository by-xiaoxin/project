<template>
	<view class="Nav" :style="'top:'+statusBarHeight+'px;'">
		<!-- 首页导航组件 -->
		<view class="Nav-img">
			<image src='../../../static/chl/chat.png' mode="scaleToFill"></image>
		</view>
		<view class="Nav-cont" @click="find">
			<image src="../../../static/chl/magnify.png"></image>智能积木 越野四驱车
		</view >
		<view class="Nav-right" @click="sm">
			<image src='../../../static/chl/scan.png' mode="scaleToFill"></image>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				statusBarHeight:0,//状态栏高度
			}
		},
		created() {
			let that = this
			
			this.statusBarHeight = uni.getSystemInfoSync().statusBarHeight+10//状态栏高度
		},
		methods:{
			find(){
				uni.navigateTo({//跳转到搜索页面
					url:'/pages/sraech/Search'
				})
			},
			sm(){//扫码
				uni.scanCode({
				    onlyFromCamera: true,
				    success: function (res) {
				        console.log('条码类型：' + res.scanType);
				        console.log('条码内容：' + res.result);
				    }
			})
			}
		}
	}
</script>

<style scopen>
	.Nav{
		display: flex;
		width: 100%;
		height: 40px;
		position: fixed;
	}
	
	.Nav-img{
		width: 15%;
		text-align: center;
	}
	
	.Nav .Nav-img image{
		width: 70upx;
		height: 70upx;
		margin-top: 5upx;
		transform: rotateY(180deg);
	}
	
	.Nav-cont{
		width: 70%;
		height: 100%;
		line-height: 80upx;
		background-color: #eee;
		color: #ccc;
	}
	
	.Nav-cont image{
		width: 40upx;
		height: 40upx;
		margin-right: 10upx;
		margin-left: 15upx;
		vertical-align: middle;
	}
	
	.Nav-right{
		width: 15%;
		height: 100%;
		text-align: center;
	}
	
	.Nav-right image{
		width: 70upx;
		height: 70upx;
		margin-top: 5upx;
	}
</style>
