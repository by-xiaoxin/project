<template>
	<view class="tabs" :style="'top:'+statusBarHeight+'px;'">
		<!-- 首页tab -->
		<view class="tabs-nav">
			<scroll-view enable-back-to-top scroll-with-animation style="width: 100%;height: 100%;" scroll-x :scroll-into-view="'act'+act">
				<view class="tabs-nav-list">
					<view :id="'act'+index" :class="[index==action?'color':'','nav-list']" v-for="(item,index) in list.category" :key="index"
					 @click="tabs(index)">
						{{item.name}}
					</view>
				</view>
			</scroll-view>
		</view>
		<view class="tabs-cont">
			<!-- tab切换页面 -->
			<swiper :current="action" @change="change" :style="'height:' +windowHeight+'px;'">
				<swiper-item>
					<view>
						<Recommend></Recommend>
					</view>
				</swiper-item>
				<swiper-item>
					<view>
						<Recommend></Recommend>
					</view>
				</swiper-item>
				<swiper-item>
					<view>
						<Recommend></Recommend>
					</view>
				</swiper-item>
				<swiper-item>
					<view>
						<Recommend></Recommend>
					</view>
				</swiper-item>
				<swiper-item>
					<view>
						<Recommend></Recommend>
					</view>
				</swiper-item>
				<swiper-item>
					<view>
						<Recommend></Recommend>
					</view>
				</swiper-item>
				<swiper-item>
					<view>
						<Recommend></Recommend>
					</view>
				</swiper-item>
			</swiper>
		</view>
	</view>
</template>

<script>
	import Recommend from "../recommend/Recommend"
	export default {
		data() {
			return {
				list: [],
				action: 0, //tab切换内容
				act:"-2",
				windowHeight:0,
				statusBarHeight:0
			}
		},
		components: {
			Recommend
		},
		methods: {
			tabs(index) {//tab切换
				this.action = index
			},
			change(e) {//改变页面
				this.action = e.detail.current
				this.act = e.detail.current-2
			}
		},
		created() {
			let that = this
			uni.request({ //列表数据
				url: "http://ceshi3.dishait.cn/api/index_category/data",
				success(res) {
					that.list = res.data.data
				}
			})
			this.windowHeight = uni.getSystemInfoSync().windowHeight-90//获取屏幕高度
			uni.getSystemInfo({
				success(res) {
					that.statusBarHeight = res.statusBarHeight+50
				}
			})
		}
	}
</script>

<style scoped>
	.tabs{
		position: fixed;
		left: 0;
		width: 100%;
		height: 100%;
	}
	
	.tabs-nav {
		width: 100%;
		height: 40px;
		margin-top: 10px;
	}

	.tabs-nav-list {
		display: flex;
		width: 140%;
		height: 100%;
	}

	.nav-list {
		width: 14.27%;
		text-align: center;
		line-height: 75upx;
		border-bottom: solid 2px #fff;
	}

	.color {
		color: red;
		border-color: red;
	}
</style>
