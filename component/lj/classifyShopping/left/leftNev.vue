<template>
	<view class="boxNev">
		<scroll-view scroll-y="true" :style="{height:gao+'px'}">
			<view class="leftNev">
				<view class="leftNev_box " :style="action == index? 'color: #FE6C05;':''" v-for="(item,index) in fen" :key="index"
				 @click="left(index)" @tap="scto">
					{{item}}{{index}}
				</view>
			</view>
			<view class="rightNev">
				<scroll-view scroll-y="true"  @scroll="scrollGet($event)" :scroll-into-view="viewId"  :style="{height:gao+'px'}">
					<view class="rightNev_3" v-for="(item,index) in img" :key="index" :id="'a'+item.id">
						<view class="rightNev_2" v-for="(itema,indexa) in item.app_category_items" :key="indexa">
							<image :src="itema.cover" mode=""></image>
							分类{{index}}:{{itema.name}}
						</view>
					</view>
				</scroll-view>
			</view>
		</scroll-view>

	</view>

</template>

<script>
	export default {
		data() {
			return {
				fen: ["分类", "分类", "分类", "分类", "分类", "分类", "分类", "分类", "分类", "分类", "分类", "分类"],
				action: 0,
				img: '',
				guli: '',
				viewId: 'a1',
				gao:'0',
				idgao:'0'
			}
		},
		methods: {
			scto: function() {//点击切换的指定ID位置
				if (this.action == 0) {
					this.viewId = 'a1'
				}
				if (this.action == 1) {
					this.viewId = 'a2'
				}
				if (this.action == 2) {
					this.viewId = 'a3'
				}
				if (this.action == 3) {
					this.viewId = 'a4'
				}
				if (this.action == 4) {
					this.viewId = 'a5'
				}
				if (this.action == 5) {
					this.viewId = 'a6'
				}
			},
			left(index) { //点击获取下标赋值
				this.action = index
			},
			scrollGet(e) {//滚动监听
			const query = uni.createSelectorQuery().in(this);//获取盒子高度
			query.select('#a1').boundingClientRect(data => {
			  
			   this.idgao = data.height
			}).exec();
				this.guli = e.target.scrollTop
				if (e.target.scrollTop < this.idgao) {
					this.action = 0
				}
				if (e.target.scrollTop > this.idgao && e.target.scrollTop < this.idgao*2) {
					this.action = 0
				}
				if (e.target.scrollTop > this.idgao && e.target.scrollTop < this.idgao*2) {
					this.action = 1
				}
				if (e.target.scrollTop > this.idgao*2 && e.target.scrollTop < this.idgao*3) {
					this.action = 2
				}
				if (e.target.scrollTop > this.idgao*3 && e.target.scrollTop < this.idgao*4) {
					this.action = 3
				}
				if (e.target.scrollTop > this.idgao*4 && e.target.scrollTop < this.idgao*5) {
					this.action = 4
				}
				if (e.target.scrollTop > this.idgao*5) {
					this.action = 5
				}
			}
		},
		created() {//数据请求
			let this_ = this
			uni.request({
				url: 'http://ceshi3.dishait.cn/api/category/app_category', //接口地址。
				// data: {
				//     name: 'name'
				// },
				// header: {
				//     'custom-header': 'hello' //自定义请求头信息
				// },
				success(res) {
					this_.img = res.data.data

					console.log(res.data.data)
				}
			});
			uni.getSystemInfo({
			　　success: function(res) { // res - 各种参数
			//        console.log(res);
			// 　　   console.log(res.screenHeight); // 屏幕的宽度 
			this_.gao = res.windowHeight-res.statusBarHeight-res.statusBarHeight
			       }
			});

			
			

		}
	}
</script>

<style scoped>
	.boxNev {
		position: fixed;
		top: 100rpx;
		width: 100%;
	}

	.leftNev {
		float: left;
	}

	.rightNev {
		position: fixed;
		left: 19%;
		width: 100%;
		display: flex;
		flex-wrap: wrap;
		height: 500upx;
	}

	.rightNev_2 {
		display: inline-block;
		width: 33.3%;
		height: 200upx;
		text-align: center;
		font-size: 30upx;
	}

	.rightNev_2 image {
		display: inline-block;
		width: 100%;
		height: 150upx;
	}

	.rightNev_3 {
		display: inline-block;
		width: 80%;
		height: 1400upx;
	}


	.leftNev_box {
		line-height: 100upx;
		height: 100upx;
		width: 100%;
		padding-left: 12%;
		border-left: solid 5upx;
	}
</style>
