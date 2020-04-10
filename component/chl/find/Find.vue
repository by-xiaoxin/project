<template>
	<view class="find">
		<!-- 查询商品和筛选组件 -->
		<view class="find-Nav">
			<view class="Nav-list" v-for="(item,index) in nav" :key="index" @click="tabs(item,index)">
				<view :class="['Nav-list-tilte',index==action?'color':'']">
					{{item.name}}
				</view>
				<view class="te">
					<view class="te-top" :style="index==action?item.top:''"></view>
					<view class="te-btn" :style="index==action?item.btn:''"></view>
				</view>
			</view>
			<view class="Nav-right" @click="screening">
				筛选
			</view>
		</view>
		<scroll-view scroll-y="true" :style="'height:'+windowHeight+'upx;'">
				<view class="find-list" v-for="(item,index) in list" :key="index" @click="tz(item.id)">
					<view class="find-list-left">
						<view class="find-list-image">
							<image :src="item.cover" ></image>
						</view>
					</view>
					<view class="find-list-right">
						<view class="right-title">
							{{item.title}}
						</view>
						<view class="right-conter">
							{{item.desc}}
						</view>
						<view class="right-btn">
							<text class="right-btn-color">￥</text>{{item.min_price}}
						</view>
						<view class="right-tto">
							1348条评论 98%满意
						</view>
					</view>
				</view>
		</scroll-view>
		<Screening :add="add" @func="func"></Screening>
	</view>
</template>

<script>
	import Screening from "../screening/Screening"
	export default {
		data() {
			return {
				list: [],
				nav: [{
						name: "综合"
					},
					{
						name: "销量"
					},
					{
						name: "价格"
					}
				],
				action: 0,//tab切换样式
				actd:{//接口data值 
					title: "",
					page: 1,
					all:"asc"
				},
				add:"100%",//左边筛选按钮弹出
				windowHeight:0
			}
		},
		
		methods: {
			func(x){//筛选组件隐藏
				this.add = x
			},
			tz(id){
				uni.navigateTo({
					url:"../../component/zmz/Particular/index/Index?id="+id+""
				})
			},
			screening(){//筛选组件出现
				this.add = "0%"
			},
			tabs(item, index) {//调整升序降序
				let slft = item
				if(index==0){
					delete this.actd.sale_count
					delete this.actd.min_price
					if(this.actd.all=="asc"){
						this.actd.all="desc"
					}else{
						this.actd.all="asc"
					}
				}
				if(index==1){
					delete this.actd.all
					delete this.actd.min_price
					if(this.actd.sale_count=="asc"){
						this.actd.sale_count="desc"
					}else{
						this.actd.sale_count="asc"
					}
				}
				if(index==2){
					delete this.actd.all
					delete this.actd.sale_count
					if(this.actd.min_price=="asc"){
						this.actd.min_price="desc"
					}else{
						this.actd.min_price="asc"
					}
				}
				if (this.action == index) {
					if(slft.top.borderBottomColor=="#F0AD4E"){
						slft.top = {
							borderBottomColor: "#CCCCCC"
						}
						slft.btn = {
							borderTopColor: "#F0AD4E"
						}
						
					}else{
						slft.top = {
							borderBottomColor: "#F0AD4E"
						}
						slft.btn = {
							borderTopColor: "#CCCCCC"
						}
					}
					
				}
				this.action = index
				this.$set(this.nav,index,slft)
				let that = this
				uni.request({
					url: "http://ceshi3.dishait.cn/api/goods/search",
					data: that.actd,
					method: "POST",
					success(res) {
						that.list = res.data.data
					}
				})
			}
		},
		computed:{
			
		},
		created() {
			let that = this
			for (var i = 0; i < that.nav.length; i++) {
				that.nav[i].top = {//添加背景颜色到对象中
					borderBottomColor: "#F0AD4E"
				}
				that.nav[i].btn = {
					borderTopColor: "#CCCCCC"
				}
			}
			
			
			this.windowHeight = uni.getSystemInfoSync().windowHeight*2-200//获取屏幕高度
		},
		mounted() {

		},
		components:{
			Screening
		},
		props:{
			val:String
		},
		watch:{
			val:{//监听数据变化刷新接口数据
				handler(a,b){
					this.actd.title=this.val
					let that = this
					uni.request({
						url: "http://ceshi3.dishait.cn/api/goods/search",
						data: that.actd,
						method: "POST",
						success(res) {
							that.list = res.data.data
							console.log(that.list)
						}
					})
				},
				immediate:true,
				deep:true
			}
		}
	}
</script>

<style scoped>
	.find{
		width: 100%;
		height: 100%;
		position: relative;
	}
	
	.find-Nav {
		display: flex;
		width: 100%;
		height: 100upx;
		border-bottom: solid 1px #CCCCCC;
		border-top: solid 1px #CCCCCC;
	}

	.Nav-list {
		width: 25%;
		line-height: 100upx;
		display: flex;
	}

	.Nav-list-tilte {
		width: 60%;
		height: 100%;
		text-align: right;
	}

	.te {
		height: 100%;
		width: 40%;
		position: relative;
	}

	.te-top {
		width: 0;
		height: 0;
		border-left: 5px solid transparent;
		border-right: 5px solid transparent;
		border-bottom: 5px solid #CCCCCC;
		display: inline-block;
		vertical-align: super;
		position: absolute;
		top: 38upx;
		left: 10upx;
	}

	.te-btn {
		width: 0;
		height: 0;
		border-left: 5px solid transparent;
		border-right: 5px solid transparent;
		border-top: 5px solid #CCCCCC;
		display: inline-block;
		vertical-align: sub;
		position: absolute;
		top: 55upx;
		left: 10upx;
	}

	.color {
		color: #F0AD4E;
	}
	
	.Nav-right{
		width: 25%;
		text-align: center;
		line-height: 100upx;
		color: #F0AD4E;
	}
	
	.find-list{
		display: flex;
		border-bottom: solid 1px #CCCCCC;
		padding: 20upx 0;
	}
	
	.find-list-left{
		width: 35%;
	}
	
	.find-list-image{
		width: 90%;
		height: 260upx;
		margin: 0 auto;
	}
	
	.find-list-image image{
		width: 100%;
		height: 100%;
	}
	
	.find-list-right{
		width: 65%;
	}
	
	.right-title{
		font-weight: 700;
		margin-top: 10upx !important;
		margin-left: 5%;
	}
	
	.right-conter{
		font-size: 30upx;
		color: #CCCCCC;
		height: 80upx;
		display: -webkit-box;
			overflow: hidden;
			-webkit-line-clamp: 2;
			-webkit-box-orient: vertical;
	}
	
	.right-tto{
		color: #CCCCCC;
		font-size: 30upx;
	}
	
	.right-btn{
		color: #F0AD4E;
	}
	
	.find-list-right view{
		margin-top: 5upx;
		width: 95%;
		margin: 5upx auto 0;
	}
	
	.right-btn-color{
		color: #F0AD4E;
		font-size: 20upx;
		vertical-align: super;
	}
</style>
