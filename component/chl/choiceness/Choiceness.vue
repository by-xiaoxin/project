<template>
	<view class="choiceness">
		<!-- 每日精选组件 -->
		<view class="choiceness-title">
			{{title}}
		</view>
		<view class="title-img">
			<image src="https://tangzhe123-com.oss-cn-shenzhen.aliyuncs.com/public/5d8833ed94392.png"></image>
		</view>
		<view class="choiceness-flex">
			<view class="choiceness-list" v-for="(item,index) in linst" :key="index" @click="tz(item.id)">
				<view class="choiceness-img">
					<image :src="item.cover"></image>
				</view>
				<view class="choiceness-introduce">
					{{item.title}}
				</view>
				<view class="choiceness-particulars">
					{{item.desc}}
				</view>
				<view class="choiceness-price">
					<text class="rmb">¥</text><text class="red">{{item.pprice}}</text>
					<text class="price">¥{{item.oprice}}</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				img: [],//顶部图片
				title: [],//顶部标题
				linst: []//商品列表
			}
		},
		onLoad() {
			
		},
		mounted() {
			let that = this
			uni.request({//每日精选商品列表
				url: "http://ceshi3.dishait.cn/api/index_category/1/data/1",
				success(res) {
					that.linst = res.data.data[4].data
					that.img = res.data.data[0].data[1].src
					that.title = res.data.data[3].data.title
				}
			})

		},
		watch: {},
		methods:{
			tz(id){
				uni.navigateTo({
					url:"../../component/zmz/Particular/index/Index?id="+id+""
				})
			}
		}
	}
</script>

<style scoped>
	/* .choiceness{
		margin-top: 20upx;
	} */

	.choiceness-title {
		text-indent: 1rem;
		font-weight: 700;
		line-height: 80upx;
	}

	.title-img {
		width: 100%;
		height: 300upx;
	}

	.title-img image {
		width: 100%;
		height: 100%;
	}

	.choiceness-flex {
		display: flex;
		flex-wrap: wrap;
		margin-top: 20upx;
	}

	.choiceness-list {
		width: 47%;
		margin-left: 2%;
	}

	.choiceness-img {
		width: 100%;
		height: 360upx;
	}

	.choiceness-img image {
		width: 100%;
		height: 100%;
	}

	.choiceness-particulars {
		text-overflow: ellipsis;
		white-space: nowrap;
		overflow: hidden;
		font-size: 28upx;
		text-indent: 0.5rem;
		color: #CCCCCC;
	}

	.choiceness-introduce {
		line-height: 60upx;
		font-size: 32upx;
		text-indent: 0.5rem;
		font-weight: 700;
	}

	.choiceness-price {
		line-height: 60upx;
		font-size: 32upx;
		text-indent: 0.5rem;
	}

	.rmb {
		color: red;
		font-size: 24upx;
		vertical-align: text-bottom;
	}

	.red {
		color: red;
	}

	.price {
		color: #CCCCCC;
		font-size: 24upx;
		margin-left: 20upx;
	}
</style>
