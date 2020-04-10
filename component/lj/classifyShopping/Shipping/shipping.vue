<template>
	<view id="main">
		<view class="mat-top">
			<view class="iocpug">购物车</view>
			<view class="ipcug" @click="mjacge">{{lakcu}}</view>
		</view>
		
		
		
		<view class="ardue">
			<view class="kacu-ra-1" v-for="(item,index) in date" :key="index" id="index">
				<view class="aocdu-icu-1">
					<view class="aitu-cig-1">
						<view class="ahd-ra-2">
							<image :src="idue" class="viace"></image>
						</view>
					</view>
					<view class="aitu-cig-2">
						<view class="ahd-ra-1">
							<image :src="item.cover" class="viace"></image>
						</view>
					</view>
				</view>
				<view class="aocdu-icu-2">
					<view class="jach-iuc-1">{{item.title}}</view>
					<view class="jach-iuc-2">{{item.skusText}}</view>
					<view class="jach-iuc-3">
						<view class="jakc-opar-1">¥ <text class="icoer">{{item.pprice}}</text></view>
						<view class="jakc-opar-2">
							<view class="kajcha-1" @click="hacuge(item)">-</view>
							<view class="kajcha-2">{{item.num}}</view>
							<view class="kajcha-1" @click="haucarc(item)">+</view>
						</view>
					</view>
				</view>
			</view>
		</view>
		
		
		
		<view class="bacurad-opra-1" v-show="gecture">
			<view class="arduce">
				<view class="aico-ye-1">
					<image src="../../static/cart-off.png" class="viace"></image>
				</view>
				<view class="aico-ye-2">购物车还是空的</view>
				<view class="aico-ye-3">去逛逛</view>
			</view>
		</view>
		<view class="opkaci">
			<view class="kacj-ice-1">为你推荐</view>
			<view class="kacj-ice-2">
				<view class="ioc-jar-1"></view>
				<view class="ioc-jar-2">买了的人还买了</view>
				<view class="ioc-jar-1"></view>
			</view>
		</view>
		
		
		
		
		
		
		
		
		
		
		
		<view class="bottom">
			<view class="bu-op-1">
				<view class="kal-opa-1">
					<view class="konge" @click="icude">
						<image :src="idue" class="viace"></image>
					</view>
				</view>
				<view class="kal-opa-2">
					<view class="aicu-ir-1">合计:</view>
					<view class="aicu-ir-2">¥0.00</view>
				</view>
			</view>
			<view class="bu-op-2">结算</view>
			<view class="aiue-kak-1" v-show="kcnueg">
				<view class="jacn-kya-1">移入收藏夹</view>
				<view class="jacn-kya-2">删除</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		data() {
			return {
				date:[],//购物车数据
				idue:"../../../../static/shoppingImg/mai.png",//全选按钮
				kmaye:true,
				lakcu:"编辑",
				kcnueg:false,
				gecture:false,
			}
		},
		methods:{
			icude(e){//全选按钮
				if(this.kmaye == true){
					this.idue = "../../../../static/shoppingImg/fill.png"
					this.kmaye = false
				}else{
					this.idue = "../../../../static/shoppingImg/mai.png"
					this.kmaye = true
				}
			},
			haucarc:function(e){//点击商品数量+1
				console.log(e)
				let _this = this;
				let car = e.id
				let vcer = e.num + 1
				   uni.request({//获取登录成功的数据
				    url: 'http://ceshi3.dishait.cn/api/login',
				    data: {
				     username: 'user2',
				     password: 'zcmcss',
					 
				    },
				    method: 'POST',
				    success(e) {
				     uni.setStorage({
				      key: 'use',
				      data: e.data.data.token
				     })
				     let str = uni.getStorage({
				      key: 'use'
				     })
				
				     str.then(function(result) {//获取购物车所有商品数据
				      uni.request({
				       url: "http://ceshi3.dishait.cn/api/cart/updatenumber/"+car+"",
					   method:"POST",
				       header: {
				        'token': result[1].data
				       },
					   data:{
						   num:vcer
					   },
				       success(data) {
						   
				       },
				       fail(e) {
				        console.log('报错')
				       }
				      })
				     })
				    }
				   })
			},
			hacuge:function(e){//点击商品数量-1
				let _this = this;
				let car = e.id
				let vcer = e.num - 1
				   uni.request({//获取登录成功的数据
				    url: 'http://ceshi3.dishait.cn/api/login',
				    data: {
				     username: 'user2',
				     password: 'zcmcss',
					 
				    },
				    method: 'POST',
				    success(e) {
				     uni.setStorage({
				      key: 'use',
				      data: e.data.data.token
				     })
				     let str = uni.getStorage({
				      key: 'use'
				     })
				
				     str.then(function(result) {//获取购物车所有商品数据
				      uni.request({
				       url: "http://ceshi3.dishait.cn/api/cart/updatenumber/"+car+"",
					   method:"POST",
				       header: {
				        'token': result[1].data
				       },
					   data:{
						   num:vcer
					   },
				       success(data) {
						 
				       },
				       fail(e) {
				        console.log('报错')
				       }
				      })
				     })
				    }
				   })
			},
			mjacge(){//编辑按钮
				if(this.lakcu == "编辑"){
					this.lakcu = "完成"
					this.kcnueg = true
				}else{
					this.lakcu = "编辑"
					this.kcnueg = false
				}
			}
		},
		onLoad:function(option){
			// uni.request({
			// 	url:"http://ceshi3.dishait.cn/api/cart",
			// 	msg:"ok",
			// 	header: {
			// 	        'token': 'ture' //自定义请求头信息
			// 	},
			// 	success: (res) => {
			// 		console.log(res)
			// 	}
				
			// })
			
			
			let _this = this;
			   uni.request({//获取登录成功的数据
			    url: 'http://ceshi3.dishait.cn/api/login',
			    data: {
			     username: 'user2',
			     password: 'zcmcss'
			    },
			    method: 'POST',
			    success(e) {
			     uni.setStorage({
			      key: 'use',
			      data: e.data.data.token
			     })
			     let str = uni.getStorage({
			      key: 'use'
			     })
			
			     str.then(function(result) {//获取购物车所有商品数据
			      uni.request({
			       url: "http://ceshi3.dishait.cn/api/cart",
			       header: {
			        'token': result[1].data
			       },
			       success(data) {
					   console.log(data)
					   if(data.data.data.length == 0){
						   _this.gecture = true
					   }else{
						   _this.gecture = false
					   }
			        _this.date = data.data.data;
					// console.log(_this.date)
			        
			       },
			       fail(e) {
			        console.log('报错')
			       }
			      })
			     })
			    }
			   })
			// uni.request({
			// 	url:"http://ceshi3.dishait.cn/api/goods/hotlist",
			// 	success: (res) => {
			// 		console.log(res)
			// 	}
			// })
			
		}
		
		
	}
</script>

<style scoped>
	#main{
		width: 745upx;
		height: 1250upx;
		border: 1px solid red;
	}
	.bottom{
		width: 100%;
		height: 120upx;
		position: fixed;bottom: 0;
		border: 1px solid #CCC;
	}
	.bu-op-1{
		width: 450upx;
		height: 120upx;
		float: left;
	}
	.bu-op-2{
		width: 290upx;
		line-height: 120upx;
		background-color: #FD6801;
		float: right;
		text-align: center;
		color: white;
		font-size: 40upx;
	}
	.kal-opa-1{
		width: 150upx;
		height: 120upx;
		float: left;
	}
	.kal-opa-2{
		width: 290upx;
		height: 120upx;
		float: left;
	}
	.konge{
		width: 50upx;
		height: 50upx;
		margin-top: 35upx;
		margin-left: 50upx;
	}
	.aicu-ir-1{
		width: 100upx;
		line-height:120upx;
		float: left;
		font-size:35upx;
		text-indent: 15upx;
		
	}
	.aicu-ir-2{
		width: 180upx;
		line-height: 110upx;
		float: left;
		color: red;
		font-size: 35upx;
		text-indent: 10upx;
	}
	.viace{
		width: 100%;
		height: 100%;
	}
	.mat-top{
		width: 100%;
		height: 60upx;
	}
	.ipcug{
		width: 100upx;
		line-height: 60upx;
		float: right;
		text-align: center;
		font-size: 33upx;
	}
	.iocpug{
		width: 630upx;
		line-height: 60upx;
		float: left;
		text-indent: 300upx;
		font-size: 35upx;
	}
	.ardue{
		width: 100%;
	}
	.bacurad-opra-1{
		width: 100%;
		height: 180upx;
		padding-top: 30upx;
	}
	.arduce{
		width: 500upx;
		height: 150upx;
		margin: auto;
	}
	.aico-ye-1{
		width: 80upx;
		height: 80upx;
		float: left;
		margin-left: 8upx;
		margin-top: 34upx;
	}
	.aico-ye-2{
		width: 280upx;
		line-height: 150upx;
		color: #CCC;
		font-size: 35upx;
		float: left;
		text-indent: 10upx;
	}
	.aico-ye-3{
		margin-top: 40upx;
		width: 110upx;
		line-height: 50upx;
		border: 2px solid #CCC;
		float: left;
		border-radius: 10upx;
		text-align: center;
		font-size: 30upx;
	}
	.opkaci{
		width: 100%;
		height: 140upx;
		background-color: #F5F5F5;
		padding-top: 50upx;
	}
	.kacj-ice-1{
		width: 100%;
		line-height: 50upx;
		text-align: center;
		font-size: 35upx;
		color: #FD6801;
	}
	.kacj-ice-2{
		width: 100%;
		height: 80upx;
	}
	.ioc-jar-1{
		width: 245upx;
		height: 20upx;
		border-bottom: 1px solid #CCC;
		float: left;
		margin-top: 14upx;
	}
	.ioc-jar-2{
		width: 250upx;
		line-height: 50upx;
		text-align: center;
		float: left;
		font-size: 30upx;
		margin-top: 10upx;
		color: #B8B8B8;
	}
	.kacu-ra-1{
		width: 745upx;
		height: 300upx;
		border-top: 1px solid #CCC;
		border-bottom: 1px solid #CCC;
	}
	.aocdu-icu-1{
		width: 340upx;
		height: 100%;
		float: left;
	}
	.aocdu-icu-2{
		width: 390upx;
		height: 100%;
		
		float: right;
	}
	.aitu-cig-1{
		width: 100upx;
		height: 300upx;
		float: left;
	}
	.aitu-cig-2{
		width: 230upx;
		height: 230upx;
		float: left;
		border: 1px solid #CCC;
		margin-top: 30upx;
	}
	.ahd-ra-1{
		width: 190upx;
		height: 190upx;
		border: 1px solid #CCC;
		margin-top: 20upx;
		margin-left: 20upx;
	}
	.ahd-ra-2{
		width: 50upx;
		height: 50upx;
		
		margin-left: 20upx;
		margin-top: 120upx;
	}
	.jach-iuc-1{
		width: 100%;
		line-height: 60upx;
		font-size: 35upx;
		margin-top: 25upx;
	}
	.jach-iuc-2{
		width: 100%;
		line-height: 50upx;
		font-size: 30upx;
		color: #838B93;
		margin-top: 20upx;
	}
	.jach-iuc-3{
		width: 100%;
		height: 80upx;
		margin-top: 20upx;
	}
	.jakc-opar-1{
		width: 160upx;
		height: 100%;
		float: left;
		font-size: 30upx;
		color: red;
	}
	.jakc-opar-2{
		width: 213upx;
		height: 70upx;
		border: 1px solid #CCC;
		float: right;
	}
	.icoer{
		font-size: 35upx;
		color: red;
	}
	.kajcha-1{
		width: 70upx;
		line-height: 70upx;
		background-color: #F8F8F8;
		color: black;
		float: left;
		font-size: 30upx;
		text-align: center;
	}
	.kajcha-2{
		width: 70upx;
		line-height: 70upx;
		float: left;
		text-align: center;
		font-size: 30upx;
		border-left: 1px solid #CCC;
		border-right: 1px solid #CCC;
	}
	.aiue-kak-1{
		width: 600upx;
		height: 100%;
		background-color: red;
		position: absolute;top: 0;right: 0;
	}
	.jacn-kya-1{
		width: 298upx;
		line-height: 120upx;
		float: left;
		color: white;
		font-size: 40upx;
		text-align: center;
		background-color: #FD6801;
	}
	.jacn-kya-2{
		width: 298upx;
		line-height: 120upx;
		float: right;
		background-color: red;
		color: white;
		font-size: 40upx;
		text-align: center;
	}
</style>
