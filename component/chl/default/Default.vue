<template>
	<view class="default">
		<scroll-view scroll-y="true" :style="'height:' +windowHeight+'px;'">
			<view class="top-title">
				热门搜索
			</view>
			<image class="ima" src="https://tangzhe123-com.oss-cn-shenzhen.aliyuncs.com/public/appindex1.jpg"></image>
			<view class="hot">
				<view :class="['hot-list','hot-list-'+index]" v-for="(item,index) in list.hot" :key="index" @click="classify(item)">
					{{item}}
				</view>
			</view>
			<view class="center-title">
				常用分类
			</view>
			<view class="classify">
				<view class="classify-list" v-for="(item,index) in list.classify" :key="index" @click="classify(item)">
					{{item}}
				</view>
			</view>
			<view class="btn-title">
				搜索记录
			</view>
			<view class="search">
				<view class="search-list" v-for="(item,index) in list.search" :key="index" @click="classify(item)">
					{{item}}
				</view>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				src: [],
				
				windowHeight: 0
			}
		},
		props:{
			list:Object
		},
		created() {
			let that = this
			uni.getSystemInfo({
				success(res) {
					that.windowHeight = (uni.getSystemInfoSync().windowHeight-res.statusBarHeight)  - 60 //获取屏幕高度
				}
			})
			
		},
		methods:{
			classify(item){
				this.$emit("classify",item)//点击分类和热门搜索传值到父组件
			}
		},
		computed:{
			
		},
		watch:{
			
			
		}
	}
</script>

<style scoped>
	/* .default{
		margin-top: 20upx;
	} */

	.top-title {
		text-indent: 1rem;
		font-weight: 700;
		line-height: 100upx;
	}

	.ima {
		width: 100%;
		height: 260upx;
	}

	.hot {
		display: flex;
		flex-wrap: wrap;
	}

	.hot-list {
		border: solid 1px #E9A8AC;
		background-color: #F8EAE9;
		padding: 15upx 15upx;
		margin: 20upx 0upx 0upx 20upx;
	}

	.hot-list-1 {
		border-color: #A4D0D1;
		background-color: #E8F6F6;
	}

	.hot-list-2 {
		border-color: #BECAA4;
		background-color: #F2F6E8;
	}

	.center-title {
		text-indent: 1rem;
		font-weight: 700;
		line-height: 100upx;
	}

	.classify {
		display: flex;
		border-bottom: solid 20upx #CCCCCC;
		flex-wrap: wrap;
		padding-bottom: 20upx;
	}

	.classify-list {
		padding: 10upx 20upx;
		margin: 20upx 0 0 20upx;
		background-color: #EEEEEE;
	}

	.btn-title {
		text-indent: 1rem;
		font-weight: 700;
		line-height: 100upx;
		border-bottom: solid 1px #CCCCCC;
	}

	.search-list {
		line-height: 100upx;
		border-bottom: solid 1px #CCCCCC;
		text-indent: 1.2rem;
	}
</style>
