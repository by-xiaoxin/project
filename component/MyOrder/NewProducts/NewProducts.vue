<template>
	<view>
		<!-- 头部开始 -->
		<view class="head_content">
			<view :class="['contents',index==leki?'contentss':'']" v-for="(item,index) in contentts" :key="index" @click="foserty(index)">{{item}}</view>
		</view>
		<!-- 头部结束 -->
		<!-- 主体开始 -->
		<view class="subject_content" v-for="(item,index) in hrisety" :key="index">
			<!-- 01图片 -->
			<view class="subject_image">
				<image :src="item.cover"></image>
			</view>
			<!-- 02文字 -->
			<view class="subject_left">
				<view class="titel_left">
					<view class="titel_top">Remi K20 Pro</view>
					<view class="titel_bottom">绞龙885 处理处理器</view>
				</view>
				<view class="titel_right">
					<view class="subject_bouuto">去购买</view>
				</view>
			</view>
			<!-- 03更多 -->
			<view class="more">了解更多<view>></view>
			</view>
		</view>
		<!-- 主体结束 -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				contentts: ["最热新品", "最近上新", "即将开售", "新品手机"],
				leki:0,
				hrisety:[]
			}
		},
		methods:{
			foserty(e){
				this.leki=e
			}
		},
		onLoad(){
			let _this=this
			uni.request({
				url: "http://ceshi3.dishait.cn/api/goods/hotlist",
				success(res) {
					console.log(res)
					console.log(_this.hrisety)
					_this.hrisety=res.data.data
				}
			})
		}
	}
</script>

<style>
	.head_content {
		width: 100%;
		height: 80upx;
		border-bottom: 1upx solid #F8F8F8;
	}

	.contents {
		width: 25%;
		line-height: 80upx;
		float: left;
		text-align: center;
		font-size: 30upx;
	}
	.contentss{
		color: #FD6801;
		border-bottom:1upx solid #FD6801;
	}
	.subject_content {
		width: 96%;
		height: 430upx;
		border-radius: 13upx;
		margin: 25upx 14.5upx;
		margin-bottom:45upx;
		border: 1upx solid #F6F6F6;
	}

	.subject_image {
		width: 100%;
		height: 215upx;
	}

	.subject_image image {
		width: 100%;
		height: 215upx;
		border-radius: 13upx 13upx 0upx 0upx;
	}

	.subject_left {
		width: 100%;
		height: 120upx;
		border-bottom: 1upx solid #F6F6F6;
	}

	.titel_left {
		float: left;
		width: 60%;
		padding-left: 20upx;
		height: 120upx;
	}

	.titel_top {
		font-size: 30upx;
		width: 100%;
		padding-top: 22upx;
	}

	.titel_bottom {
		font-size: 25upx;
		color: #C7C7C7;
		padding: 9upx 0upx;
	}

	.titel_right {
		float: right;
		width: 20%;
		height: 120upx;
	}

	.subject_bouuto {
		width: 78%;
		height: 59upx;
		line-height: 59upx;
		font-size: 25upx;
		background-color: #FD6801;
		color: #FFFFFF;
		border-radius: 30upx;
		text-align: center;
		margin-top: 30.5upx;
		margin-left: 10upx;
	}

	.more {
		width: 100%;
		height: 95upx;
		text-align: center;
		line-height: 95upx;
		font-size: 30upx;
		border-radius: 0upx 0upx 13upx 13upx;
		position: relative;
		box-shadow: 0px 2px 1px 1px #EBEDEE;
	}

	.more view {
		font-size: 50upx;
		color: #B2B2B2;
		position: absolute;
		right: 36%;
		top: 0%;
	}
</style>