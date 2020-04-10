<template>
	<view>
		<!-- 头部开始 -->
		<view class="head_content">
			<view v-for="(tabBar,index) in content" :key="index" :class="['swiper-tab-list',tabIndex==index?'active':'']" @click="toggleTab(index)">
				{{tabBar}}
				<view :class="{'swiper-tab-line': tabIndex==index}"></view><!-- {'active': tabIndex==index} -->
			</view>
		</view>
		<!-- 头部结束 -->
		<!--内容区-->
		<!-- <view> -->
		<!-- <Message></Message> -->
		<!-- </view> -->
		<view class="result">
			<view class="result_01">
				<swiper :current="tabIndex" @change="tabChange" style="height:480rpx;">
					<swiper-item>
						<view class="list">
							<Message></Message>
						</view>
					</swiper-item>
					<swiper-item>
						<view class="list"></view>
					</swiper-item>
					<swiper-item>
						<view class="list"></view>
					</swiper-item>
					<swiper-item>
						<view class="list"></view>
					</swiper-item>
				</swiper>
			</view>
		</view>
		<view>
			<Like></Like>
		</view>
	</view>
</template>

<script>
	import Like from '../Like/Like.vue';
	import Message from '../Message/Message.vue';

	let app = getApp();
	export default {
		data() {
			return {
				tabIndex: 0, //选中标签栏的序列
				content: ["全部", "待付款", "待收货", "待评价"],
				listHeight: 0,
				swiperHeight: 0,
			}
		},
		methods: {
			toggleTab(index) {
				// console.log(index)
				this.tabIndex = index
			},
			//滑动切换swiper
			tabChange(e) {
				console.log(e.detail)
				// const tabIndex = e.detail.current
				this.tabIndex = e.detail.current
			},
		},
		onLoad(options) {
			let _this = this
			console.log(options.id)
			_this.tabIndex = options.id	
		},
		components: {
			Like,
			Message
		},
		// onLoad(){
		// 	uni.request({
		// 		url: "http://ceshi3.dishait.cn/api/order/",
		// 		data:{
		// 			type:'paying'
		// 		},
		// 		header:{
		// 			token:'7dadcf0161710b5256265ed25cb7873b3fd61633'
		// 		},
		// 		method:'POST',
		// 		success(res) {
		// 			console.log(res)
		// 		}
		// 	})
		// }
	}
</script>

<style>
	.head_content {
		width: 100%;
		height: 90upx;
	}

	.swiper-tab-list {
		width: 25%;
		line-height: 90upx;
		text-align: center;
		font-size: 30upx;
		float: left;
		color: #BEBEBE;
	}

	.result {
		width: 100%;
		background-color: #F5F5F5;
		display: inline-block;
	}

	/* .list{
		height:1000rpx;
	} */
	.result_01 {
		width: 100%;
		display: inline-block;
	}

	/* .swiper{ */
	/* display:flex;
		flex: 1 1 auto; */
	/* width:100%; */
	/* height:auto; */
	/* display:inline-block!important; */
	/* height:100%; */
	/* height:0rpx!important; */
	/* } */
	/* swiper-item{
		height:auto;
	} */
	/* swiper :first-child{
	position: absolute;
	} */
	/* .uni-swiper-tab {
		width: 100%;
		height: 90rpx;
		
	}
	
	.swiper-tab-list{ */
	/* width:25%; */
	/* 	line-height: 90rpx;
		font-size:30rpx;
		text-align: center;
	} */
	/* .swiper-tab-list{ */
	/* width:30%; */
	/* line-height: 90rpx; */
	/* 	float:left;
		font-size:30rpx;
		text-align: center;
	} */
	/* .swiper-tab-list {
		color: #969696;
		font-weight: bold;
	} */
	.active {
		color: #F66A08;
	}

	.swiper-tab-line {
		border-bottom: 1upx solid #F66A08;
	}
</style>
