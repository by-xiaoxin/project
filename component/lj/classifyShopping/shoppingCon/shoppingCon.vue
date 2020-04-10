<template>
	<view class="box">
		<view class="topNev" style="position: fixed; top: 0; background-color: #FFFFFF;z-index: 100;">
			<view class="ltop">
				购物车
			</view>
			<view class="righ"  @click="bianji">
				{{bian}}
			</view>
		</view>
		<view class="content" :style="dad !== ''? 'display: none;':''">
			<view class="imggg">
				<image src="../../../../static/shoppingImg/3.1gw.png" mode=""></image>
			</view>
			<view class="zi">
				购物车还是空的
			</view>
			<view class="cil">
				去逛逛
			</view>

		</view>
		<view class="ardue">
			<view class="kacu-ra-1" v-for="(item,index) in dad" :key="index">
				<view class="aocdu-icu-1">
					<view class="aitu-cig-1">
						<view class="ahd-ra-2"  >
							<image class="viace" v-if="item.checked" @click="handleSelectRadio(index)" src="../../../../static/shoppingImg/fill.png"></image>
								<image  class="viace" v-else @click="handleSelectRadio(index)" src="../../../../static/shoppingImg/mai.png"></image>
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
							<!-- 加减数量 -->
							<view class="kajcha-1"@click="reduction(index)">-</view>
							<view class="kajcha-2">{{item.num}}</view>
							<view class="kajcha-1"@click="add(index)">+</view>
						</view>
					</view>
				</view>
			</view>
		</view>
		<view class="bottom" :style="{top:gao+'px'}"><!-- 计算价格 删除 -->
			<view class="bu-op-1">
				<view class="kal-opa-1">
					<view class="konge">
						<!--全选按钮-->
						<image class="viace" v-if="kmaye1" @click="handlekmaye1" src="../../../../static/shoppingImg/fill.png"></image>
							<image class="viace" v-else @click="handlekmaye1" src="../../../../static/shoppingImg/mai.png"></image>
					</view>
				</view>
				<view class="kal-opa-2">
					<view class="aicu-ir-1" style="margin-top: 30upx;">合计:<text style="color: #F86A06;">¥{{money}}</text></view>
				</view>
			</view>
			<view class="bu-op-2">结算</view>
			<view class="aiue-kak-1" v-show="kcnueg">
				<view class="jacn-kya-1">移入收藏夹</view>
				<view class="jacn-kya-2" @click="handleDel">删除</view>
			</view>
		</view>
		<!-- 弹窗 -->
		<!-- <popup-select :fixd="fixd" :carList='carLists[ind]' :selectCarListConfig="selectCarListConfig" @handleCloseCar='handleCloseFixd'></popup-select>
		<view style="height:88upx;width: 100%;"></view>
		<view class="mark" v-show="fixd" @click="handleCloseFixd"></view> -->
	</view>

</template>

<script>
	
	
	export default {
		data() {
			return {
				checked: '',
				disabled: 'true',
				dad:'',
				kmaye:true,
				bian:"编辑",
				kcnueg:false,
				kmaye1:false,//全选按钮
				gecture:false,
				money:0.00.toFixed(2),//总价
				gecture:false,
				gao:'0',
				yaoshi:'',
			}
		},
		methods: {
			handleEditor() {//点击编辑文本切换  并显示收藏和删除
				let that = this;
				this.editorColle = !this.editorColle;
				this.versionSelection = !this.versionSelection;
				if(this.dad.length == 0){  //列表为空时全选按钮为false
					this.kmaye1 = false;
				}
			},
			handleSelectRadio(e) {//单选中  全部选中时全选选中
				let that = this;
				that.dad[e].checked = !that.dad[e].checked; //反选
				for (let i = 0; i < that.dad.length; i++) {
					if (!that.dad[i].checked) {
						that.kmaye1 = true;
					}
				}
				that.kmaye1 = !that.kmaye1;
				this.comBined();
			},
			handlekmaye1(){//全选选中时 让所有商品也选中
				let that = this;
				that.kmaye1 = !that.kmaye1;
				for (let i in that.dad) {
					that.dad[i].checked = that.kmaye1;
				}
				if(this.dad.length == 0){  //列表为空时全选按钮为false
					this.kmaye1 = false;
				}
				this.comBined();
			},
			reduction (e){//减少数量 当数量等于最小值时就等于最小值
				let that = this;
				if(that.dad[e].num > that.dad[e].minnum){
					that.dad[e].num = that.dad[e].num - 1;
					this.comBined();
				}
			},
			add(e){//点击添加数量
				let that = this;
				if(that.dad[e].num < that.dad[e].maxnum){
					that.dad[e].num ++;
					this.comBined();
				}
			},
			comBined(){//计算总计价格
				let nmb = 0;
				for (var j = 0; j < this.dad.length; j++) {
					if(this.dad[j].checked){
						for (var i = 0; i < this.dad.length; i++) {
							if(this.dad[i].checked){
								nmb += this.dad[i].pprice * this.dad[i].num;
								this.money = parseFloat(nmb.toFixed(2));
							}
						}
						return
					}
				}
				this.money = 0;
			},
			handleDel(){
				/** 
				 * 点击删除选中列表
				 */
				let that = this;
				for (var i = 0; i < that.dad.length; i++) {
					if(that.dad[i].checked){
						uni.request({
							url:'http://ceshi3.dishait.cn/api/cart/delete',
							method:'POST',
							header:{
								token : '34bcdb90950f8a2a3e71a4f0f1e1d4acc9c2aaa4'
							},
							data:{
								shop_ids : that.dad[i].id
							},
							success: (res) => {
								that.created();
							}
						})
					}
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
				       success(res) {
						    
				       },
				       fail(e) {
				        console.log('报错')
				       }
				      })
				     })
				    }
				   })
				   this.comBined();
				   
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
				       success(res) {
						 
				       },
				       fail(e) {
				        console.log('报错')
				       }
				      })
				     })
				    }
				   })
				   this.comBined();
			},
			handleSkus(e){//e 获取到当前数据下标点击选项弹窗

				uni.showLoading({
					title:'加载ing',
					mask:true
				})
				this.ind = e;
				this.fixd = true;
				let LIstId = this.carLists[e].id;
				uni.request({  //发送点击的数据id获取库存
					url:`http://ceshi3.dishait.cn/api/cart/${LIstId}/sku`,
					header:{
						token : '7dadcf0161710b5256265ed25cb7873b3fd61633'
					},
					success:(res) => {
						this.selectCarListConfig = res.data.data;
						uni.hideLoading();
					}
				})
			},
			handleCloseFixd(){点击mark隐藏蒙版和弹窗
				this.fixd = false;
			},
			bianji(){//编辑按钮
				if(this.bian == "编辑"){
					this.bian = "完成"
					this.kcnueg = true
				}else{
					this.bian = "编辑"
					this.kcnueg = false
				}
			}
		},
		created() { //数据请求
		
		let this_= this
		uni.getStorage({
		key:"miyao",
		success(e){
			console.log(e.data.data)
		this_.yaoshi = e.data.data.token//这就是你想要取的token
		console.log(this_.yaoshi)
		}
		});
			uni.request({
				
				url: 'http://ceshi3.dishait.cn/api/cart', //接口地址。
				data: {
					msg: 'ok'
				},
				header: {
					'token': '34bcdb90950f8a2a3e71a4f0f1e1d4acc9c2aaa4' //请求头信息
				},
				success: (res) => {
					this_.dad = res.data.data
				},
			});
			
			uni.getSystemInfo({
			　　success: function(res) { // res - 各种参数
			       console.log(res);
			　　   console.log(res.screenHeight); // 屏幕的宽度 
			this_.gao = res.windowHeight-53
			       }
			});
		},


	}
</script>

<style scoped>
	.content {
		display: flex;
		justify-content: center;
		line-height: 200upx;
		text-align: center;
		margin-top: 120upx;
	}

	.imggg image {
		width: 55upx;
		height: 55upx;
	}

	.zi {
		width: 300upx;
		color: #999999;
		font-size: 35upx;
	}

	.boxshooping {
		width: 100%;
		height: 350upx;
		background-color: #007AFF;
	}
	.viace{
		width: 100%;
		height: 100%;
	}
	.bottom{
		background-color: #FFFFFF;
		width: 100%;
		height: 120upx;
		bottom: 100upx;
		position: fixed;
		z-index: 100;
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
	.ardue{
		width: 100%;
		margin-top: 120upx;
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
		margin-top: 30upx;
	}
	.ahd-ra-1 image{
		width: 190upx;
		height: 190upx;
		margin-top: 20upx;
		margin-left: 20upx;
	}
	.ahd-ra-2 {
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
	.topNev{
		line-height: 120upx;
		width: 100%;
	}
	.ltop{
		display: inline-block;
		margin-left: 40%;
		width: 40%;
	}
	.righ{
		width: 20%;
		
		float: right;
	}
	.konge{
		width: 50upx;
		height: 50upx;
		margin-top: 35upx;
		margin-left: 50upx;
	}
</style>
