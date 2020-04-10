<template>
	<view class="search" :style="'top:'+statusBarHeight+'px;'">
		<!-- 搜索主页面 -->
		<view class="Nav">
			<view class="Nav-left">
				<image src='../../static/chl/back.png' mode="scaleToFill" @click="bt"></image>
			</view>
			<view class="Nav-center">
				<input :value="val" @input="inptu" type="text" placeholder-style="text-indent: 2rem;" placeholder="智能积木 越野四驱车" />
				<image v-if="show" src='../../static/chl/magnify.png'></image>
			</view>
			<view class="Nav-right" @click="search">
				搜索
			</view>
		</view>
		<view class="mian">
			<Default v-if="hide" @classify="classify" :list="list"></Default>
			<Find v-if="hideh" :val="val"></Find>
			<Found v-if="hidee"></Found>
		</view>
	</view>
</template>

<script>
	import Default from '../../component/chl/default/Default'
	import Find from '../../component/chl/find/Find'
	import Found from "../../component/chl/found/Found"
	export default {
		data() {
			return {
				val: "", //传递参数
				show: true, //控制搜索放大镜图片显示隐藏
				hide: true, //控制搜索前页面显示
				hideh: false, //控制搜索后页面显示
				hidee: false, //搜索不到商品
				statusBarHeight: 0, //状态栏高度
				top: 0,
				defa:'',
				list: {
					hot: ["领劵中心", "Redmi K20", "RedmiBook 14", "智能积木 越野四驱车", "手环 腕带"],
					classify: ["耳机", "手机", "音箱", "手表", "配件", "网关/传感器", "健康", "酷玩"],
					search: ["小米", "小米8 屏幕指纹版"]
				}
			}
		},
		components: {
			Default,
			Find,
			Found
		},
		onLoad(opaitn) {
		},
		methods: {
			classify(data) {//子组件传事件，改搜索框的value值
				this.val = data
				let a = {
					detail: {
						value: data
					}
				}
				this.inptu(a)
				let bool = false
				this.list.search.forEach((item,index)=>{
					if(data.indexOf(item)>=0){
						bool = true
					}
				})
				if(!bool){
					this.list.search.push(data)
				}
			},
			inptu(e) {
				let that = this
				let bool = false
				
				if (e.detail.value == "") {
					that.val = e.detail.value
					that.hide = true
					that.hideh = false
					that.hidee = false
					that.show = true
					return
				} else {
					this.list.search.forEach((item,index)=>{
						if(e.detail.value.indexOf(item)>=0){
							bool = true
						}
					})
					if(!bool){
						this.list.search.push(e.detail.value)
					}
					uni.request({
						url: "http://ceshi3.dishait.cn/api/goods/search",
						data: {
							title: e.detail.value,
							page: 1,
						},
						header: {
							'content-type': 'application/x-www-form-urlencoded', 
						},
						method: "POST",
						success(res) {
								that.show = false
								that.val = e.detail.value
								if(res.statusCode == 200){
									if(res.data.data.length>0){
										that.hide = false
										that.hideh = true
										that.hidee = false
									}else{
										that.hide = false
										that.hideh = false
										that.hidee = true
									}
								}else{
									that.hide = false
									that.hideh = false
									that.hidee = true
								}
						},
						fail(res) {
							that.show = false
							that.hide = false
							that.hideh = false
							that.hidee = true
						}
					})
				}
			},
			search() {

			},
			bt() {
				uni.navigateBack({
					
				})
			}
		},
		created() {
			let that = this
			this.statusBarHeight = uni.getSystemInfoSync().statusBarHeight+10//状态栏高度

		}
	}
</script>

<style scoped>
	.search {
		position: fixed;
		left: 0;
		width: 100%;
		height: 100%;
	}

	.Nav {
		display: flex;
		width: 100%;
		height: 80upx;
		padding-bottom: 20upx;
		left: 0;
	}

	.Nav-left {
		width: 15%;
		text-align: center;

	}

	.Nav-left image {
		width: 40upx;
		height: 40upx;
		margin-top: 20upx;
	}

	.Nav-center {
		width: 70%;
		height: 100%;
		background-color: #EEEEEE;
		position: relative;
	}

	.Nav-center image {
		width: 40upx;
		height: 40upx;
		position: absolute;
		top: 20upx;
		left: 30upx;
	}

	.Nav-right {
		width: 15%;
		text-align: center;
		line-height: 80upx;
	}

	.Nav input {
		width: 96%;
		height: 100%;
		margin: 0 auto;

	}



	.cass {
		background-image: url(../../static/chl/magnify.png);
		background-position: 0px 0px;
		text-indent: 1rem;
	}
</style>
