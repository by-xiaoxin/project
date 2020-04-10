<template>
	<view class="screening" :style="'left:'+add" >
		<!-- 筛选组件 -->
		<view class="screening-left" @click="top">
		</view>
		<view class="screening-right">
			<view class="screening-top">
				<view class="screening-title">
					服务
				</view>
				<view class="screening-list">
					<view @click="tabs(index)" :class="['screening-list-center',index==action?'color':'']" v-for="(item,index) in list.top" :key="index">
						{{item}}
					</view>
				</view>
				<view class="screening-title">
					分类
				</view>
				<view class="screening-list">
					<view @click="tabd(index)" :class="['screening-list-center',index==actidn?'color':'']" v-for="(item,index) in list.btn" :key="index">
						{{item}}
					</view>
				</view>
			</view>
			<view class="btn">
				<view class="btn-left" @click="reset">
					重置
				</view>
				<view class="btn-right" @click="top">
					确定
				</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default{
		data(){
			return{
				list:{
					top:["促销","分期","仅看有货"],
					btn:["耳机","户外","配件"]
				},
				action:0,//服务下标
				actidn:0//分类下标
			}
		},
		props:{
			add:String
		},//控制滑入滑出
		watch:{
			
		},
		methods:{
			tabs(index){
				this.action = index
			},
			tabd(index){
				this.actidn = index
			},
			top(){
				this.$emit('func',"100%")
			},
			reset(){
				this.action = 0
				this.actidn = 0
			}
		}
	}
</script>

<style scoped>
	.screening{
		position: absolute;
		top: 0;
		width: 100%;
		height: 100%;
		transition-duration: 0.5s;
		display: flex;
	}
	
	.screening-top{
		width: 100%;
		height: 90%;
	}
	
	
	.screening-left{
		width: 25%;
		background-color: rgba(0,0,0,0.4);
		height: 100%;
	}
	
	.screening-right{
		width: 75%;
		height: 100%;
		background-color: #FFFFFF;
		z-index: 100;
	}
	
	.screening-title{
		width: 90%;
		margin: 0upx auto 0;
		line-height: 100upx;
		
	}
	
	.screening-list{
		width: 90%;
		margin: 0 auto;
		display: flex;
	}
	
	.screening-list-center{
		border: solid 1px #FFFFFF;
		background-color: #EEEEEE;
		padding: 15upx 30upx;
		margin: 0 20upx 0 0;
		font-size: 30upx;
	}
	
	.color{
		border-color: #E47930;
		background-color: #FCE0D5;
		color: #E47930;
	}
	
	.btn{
		display: flex;
		width: 100%;
		height: 10%;
	}
	
	.btn-left{
		width: 50%;
		height: 100%;
		padding: 5% 0;
		text-align: center;
	}
	
	
	.btn-right{
		width: 50%;
		height: 100%;
		background-color: #FD6801;
		padding: 5% 0;
		text-align: center;
		color: #FFFFFF;
	}
	
</style>
