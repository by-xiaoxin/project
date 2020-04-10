<template>
	<view class="recommend">
		<!-- 首页推荐页面 -->
		<scroll-view class="scroll-y" scroll-y :style="'height:'+windowHeight+'px'">
			<view class="scoll-Nav" >
				<view class="carousel">
					<swiper class="swiper" autoplay circular @change="tabs" >
						<swiper-item v-for="(item,index) in carousel" :key="index">
							<view class="ima">
								<image mode="scaleToFill" :src="item.src"></image>
							</view>
						</swiper-item>
					</swiper>
					<view class="point">
						<view :class="['point-top',index==act?'color':'']" v-for="(item,index) in 3" :key="index">
						</view>
					</view>
				</view>
				<view class="sort">
					<view class="sort-list" v-for="(item,index) in list" :key="index"> 
						<view class="sort-img">
							<image mode="scaleToFill" :src="item.src"></image>
						</view>
						<view class="sort-title">
							{{item.text}}
						</view>
					</view>
				</view>
				<view class="three">
					<view :class="'image'+index" v-for="(item,index) in exhibition" :key="index">
						<image :src="item.src" mode="scaleToFill" ></image>
					</view>
				</view>
				<Choiceness></Choiceness>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	import Choiceness from "../choiceness/Choiceness"
	export default {
		data() {
			return {
				list: [],//分类列表
				act: 0,
				carousel:[],//轮播
				exhibition:[],//展示图片
				windowHeight:0,//可显示高度
				statusBarHeight:0
			}
		},
		created() {
			let action = this.action + 1
			let that = this
			uni.request({//获取推荐数据
				url: "http://ceshi3.dishait.cn/api/index_category/1/data/1",
				success(res) {
					that.list = res.data.data[1].data
					that.carousel = res.data.data[0].data
					that.exhibition = res.data.data[2].data
				}
			})
			uni.getSystemInfo({
				success(res) {
					that.statusBarHeight = res.statusBarHeight+10
				}
			})
			this.windowHeight = uni.getSystemInfoSync().windowHeight-this.statusBarHeight-40
			
		},
		components:{
			Choiceness
		},
		methods: {
			tabs(e) {//切换轮播图片改变指示点样式
				this.act = e.detail.current
			}
		}
	}
</script>

<style scoped>
	.swiper{
		height: 360upx !important;
	}
	
	.recommend {
		width: 100%;
		height: 100%;
	}

	.carousel {
		position: relative;
	}
	
	.scoll-Nav{
		height: 3400upx;
	}
	
	.ima{
		width: 100%;
		height: 100%;
	}

	.ima image {
		width: 100%;
		height: 100%;
	}

	.point {
		position: absolute;
		top: 90%;
		right: 5%;
	}

	.sort-img image {
		width: 60upx;
		height: 60upx;
	}
	
	.sort-title{
		font-size: 24upx;
		padding-top: 10upx;
	}

	.point-top {
		width: 20upx;
		height: 20upx;
		border-radius: 50%;
		background-color: #666;
		float: left;
		margin-left: 10upx;
		z-index: 100;
	}

	.color {
		background-color: #fff
	}

	.sort {
		display: flex;
		flex-wrap: wrap;
		margin-top: 10upx;
	}

	.sort-list {
		width: 20%;
		text-align: center;
		padding: 20upx 0;
	}
	
	.three{
		width: 100%;
		height: 500upx;
	}
	
	.three image{
		width: 100%;
		height: 100%;
		
	}
	
	.image0{
		width: 49%;
		height: 500upx;
		float: left;
	}
	
	.image1{
		width: 49%;
		height: 245upx;
		float: right;
	}
	
	.image2{
		width: 49%;
		height: 245upx;
		margin-top: 10upx;
		float: right;
	}
</style>
