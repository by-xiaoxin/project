<template>
	<view class="main">
		<!-- 第一小部分 -->
		<!-- 商品图片 -->
		<view class="goodsimg">
			<swiper indicator-dots="true">
				<swiper-item v-for="(item,index) in datas.goodsBanner" :key="index">
					<image :src="datas.cover"></image>
				</swiper-item>
			</swiper>
		</view>
		<!-- 商品名字-->
		<view class="goodsna">
			{{datas.title}}
		</view>
		<!-- 商品介绍 -->
		<view class="goodsin">
			{{datas.desc}}
		</view>
		<!-- 商品价格 -->
		<view class="goodspr">
			￥<text>{{datas.min_price}}</text>
		</view>
		<!-- 选择商品类型 -->
		<scroll-view scroll-x="true" class="goodstyd">
			<view class="goodstys" v-for="(item,index) in datas.goodsAttrs" :key="index">
				<view class="goodsty">
					<image src="../../../../static/zmz/img/CPU.png"></image>
				</view>
				<view class="goodstyn">{{item.name}}</view>
				<view class="goodstyv">{{item.value}}</view>
			</view>
		</scroll-view>
		<!-- 第二小部分 -->
		<view class="choice">
			<view class="part1" @click="showup(1)">
				<view class="partl">
					已选<text v-for="(item,index) in pick" :key=index>{{item.dcolor}}</text>
				</view>
				<view class="partr">
					>
				</view>
			</view>
			<view class="part2" @click="showup(2)">
				<view class="partl">
					配送<text>北京</text><text>东城</text><text class="last">有现货</text>
				</view>
				<view class="partr">
					>
				</view>
			</view>
			<view class="part3" @click="showup(3)">
				<view class="partl">
					<text><text class="smis">√</text>小米自营</text>
					<text><text class="smis">√</text>小米发货</text>
					<text><text class="smis">√</text>七天无理由退货</text>
				</view>
				<view class="partr">
					>
				</view>
			</view>
		</view>
		<!-- 第三小部分 -->
		<scroll-view scroll-x="true" class="comments">
			<view class="commentsson" v-for="(item,index) in hotcomments" :key="index">
				<view class="commenter">
					<view class="ctop">
						<view class="commenterimg">
							<image src="../../../../static/zmz/img/head.jpg"></image>
						</view>
						<view class="commentername">
							{{item.user.nickname}}
							<view class="date">
								2019-06-20
							</view>
						</view>
						<view class="good">
							<image src="../../../../static/zmz/img/good.png"></image>
							{{item.id}}
						</view>
					</view>
					<view class="ccenter">
						{{item.review.data}}
					</view>
					<view class="cbottom" v-for="(im,ind) in item.review.image" :key="index">
						<image :src="im"></image>
					</view>
				</view>
			</view>
		</scroll-view>
		<view class="morecom">
			更多评论>
		</view>
		<!-- 商品详情图片 -->
		<view class="cimg">
			<image v-for="(item,index) in datas.goodsBanner" :key="index" :src="item.url" ></image>
		</view>
		<!-- 第四小部分 -->
		<view class="maybelike">
			<view class="mltitle">
				为你推荐
			</view>
			<view class="rec">
				<view class="recson" v-for="(item,index) in amybelike" v-if="index<4" :key="index" @click="sdot(item.id)">
					<view class="recimg">
						<image :src="item.cover"></image>
					</view>
					<view class="rectit">
						{{item.title}}
					</view>
					<view class="recind">
						{{item.desc}}
					</view>
					<view class="recpri">
						￥<text class="min_price">{{item.min_price}}</text>
						<text class="min_oprice">￥{{item.min_oprice}}</text>
					</view>
				</view>
			</view>
		</view>
		
		<!-- 加入购物车 -->
		<view class="addshopcar">
			<view class="collect">
				<view class="img">
					<image src="../../../../static/zmz/img/love.png"></image>
				</view>
				收藏
			</view>
			<view class="shopcar">
				<view class="img">
					<image src="../../../../static/zmz/img/shpocar.png"></image>
				</view>
				购物车
			</view>
			<view class="addsc" @click="nones">
				加入购物车
			</view>
		</view>
		<!-- 遮罩层 -->
		<view :class="['cover',show?'show':'']"></view>
		<pop-up :show="show" :ids="ids" :nums="nums"  @nones="nones"  @lose="lose"></pop-up>
	</view>
</template>

<script>
	import PopUp from '../../com/Com.vue'
	export default {
		data() {
			return {
				datas: {},
				pick: [],
				hotcomments: [],
				amybelike: [],
				show:false,
				nums:0,
				num:1,
				ids:25
			}
		},
		components:{
			PopUp
		},
		onLoad() {
			// console.log(this.datas.goodsBanner)
			let _this = this
			// 指定商品详情
			let list = []
			uni.request({
				url: "http://ceshi3.dishait.cn/api/goods/25",
				success(res) {
					_this.datas = res.data.data
					_this.pick = _this.datas.goodsSkusCard
					if(_this.datas.hotComments.length<=0){
						_this.hotcomments = [{review:{data:"暂时没有评价~~"},image:[],user:{nickname:""},id:""}]
					}else{
						_this.hotcomments = _this.datas.hotComments
					}
					for (var i = 0; i < _this.pick.length; i++) {
						for (var j = 0; j < _this.pick[i].goodsSkusCardValue.length; j++) {
							_this.pick[i].goodsSkusCardValue[j].key = false
						}
						_this.pick[i].goodsSkusCardValue[0].key = true
						list.push(_this.pick[i].goodsSkusCardValue[0].value)
					}
					for (var i = 0; i < list.length; i++) {
						_this.pick[i].dcolor = list[i]
					}
				}
			})
			// 猜你喜欢
			uni.request({
				url: "http://ceshi3.dishait.cn/api/goods/hotlist",
				success(res) {
					_this.amybelike = res.data.data
				}
			})

		},
		methods: {
			showup: function(nums) {
				this.show = true
				this.nums = nums
			},
			sdot:function(id){
				let _this = this
				// 指定商品详情
				let list = []
				uni.request({
					url: "http://ceshi3.dishait.cn/api/goods/"+id+"",
					success(res) {
						console.log(res)
						_this.datas = res.data.data
						_this.pick = _this.datas.goodsSkusCard
						if(_this.datas.hotComments.length<=0){
							_this.hotcomments = [{review:{data:"暂时没有评价~~"},image:[],user:{nickname:""},id:""}]
						}else{
							_this.hotcomments = _this.datas.hotComments
						}
						for (var i = 0; i < _this.pick.length; i++) {
							for (var j = 0; j < _this.pick[i].goodsSkusCardValue.length; j++) {
								_this.pick[i].goodsSkusCardValue[j].key = false
							}
							_this.pick[i].goodsSkusCardValue[0].key = true
							list.push(_this.pick[i].goodsSkusCardValue[0].value)
						}
						for (var i = 0; i < list.length; i++) {
							_this.pick[i].dcolor = list[i]
						}
					}
				})
			},
			nones:function(datas){
				let _this = this
				if(datas.datas){
					_this.num = datas.num
					_this.show = datas.show
					for (var i = 0; i < datas.datas.length; i++) {
						_this.pick[i].dcolor = datas.datas[i]
					}
				}
				uni.request({
					url: "http://ceshi3.dishait.cn/api/cart",
					header: {
						token: '7dadcf0161710b5256265ed25cb7873b3fd61633'
					},
					method: 'POST',		
					data:{
						shop_id:_this.datas.goods_type_id,
						skus_type:_this.datas.express_id,
						num:_this.num
					},
					success(res) {
						console.log(res)
					}
				})	
			},
			lose:function(data){
				this.show = data.show
			}
		}
	}
</script>

<style>
	.main {
		padding: 0px 16upx;
	}
	.cover {
		width: 100%;
		height: 100vh;
		background-color: rgba(0, 0, 0, 0.5);
		position: fixed;
		top: 0px;
		display: none;
	}
	/* 第一小部分 */
	.goodsimg image {
		width: 100%;
		height: 480upx;
		text-align: center;
	}
	swiper-item,swiper{
		height: 480upx;
		width: 100%;
	}

	.goodsna {
		font-size: 42upx;
		margin: 14upx 0px;
	}

	.goodsin {
		font-size: 32upx;
		color: #C9C9C9;
	}

	.goodspr {
		color: #F86A07;
		font-size: 24upx;
		vertical-align: top;
		margin: 20upx 0px;
	}

	.goodspr text {
		font-size: 38upx;
		font-weight: bold;
		vertical-align: middle;
	}

	.goodstyd,
	.comments {
		white-space: nowrap;
	}

	.goodstys {
		width: 24%;
		display: inline-block;
	}

	.goodstyn {
		font-size: 30upx;
		font-weight: bold;
	}

	.goodstyv {
		font-size: 24upx;
		color: #C0C0C0;
	}
	.goodsty image{
		width: 60upx;
		height: 60upx;
	}
	.img image{
		width: 40upx; height: 40upx;
	}
	/* 第二小部分 */
	.choice {
		padding: 0px 15upx;
		background-color: #F5F5F3;
		border-radius: 5px;
		border: 1px solid #F1F1F1;
	}

	.choice view {
		height: 100upx;
		line-height: 100upx;
		border-bottom: 1px solid #F1F1F1;
	}

	.part1,
	.part2 {
		font-size: 32upx;
		color: #858585;
		display: flex;
	}

	,
	.part3 {
		font-size: 28upx;
		color: #858585;
		display: flex;
	}

	.partl {
		width: 86%;
	}

	.partr {
		width: 10%;
		font-size: 34upx;
	}

	.choice text {
		margin: 0px 10upx;
	}

	.last {
		color: #E67524;
	}
	.smis{background-color: #EF5300; border-radius: 50%; color: white; margin: 0px; padding: 4upx 6upx;
	font-size: 26upx;}
	/* 第三小部分 */
	.commentsson {
		width: 80%;
		background-color: #F5F5F3;
		border-radius: 20upx;
		margin: 10upx;
		display: inline-block;
		padding: 20upx;
	}

	.ctop {
		display: flex;
	}

	.commenterimg {
		width: 15%;
	}

	.commenterimg image {
		width: 80%;
		height: 70upx;
		border-radius: 50%;
	}

	.commentername {
		font-size: 30upx;
		width: 65%;
	}

	.date {
		font-size: 24upx;
		color: #CFCFCF;
	}

	.good {
		width: 15%;
		font-size: 30upx;
		text-align: right;
		color: #CFCFCF;
	}

	.ccenter {
		font-size: 32upx;
		line-height: 70upx;
	}

	.cbottom image {
		width: 40%;
		height: 80upx;
	}

	.morecom {
		line-height: 60upx;
		color: #3994F1;
		font-weight: bold;
		text-align: center;
		font-size: 30upx;
	}

	.cimg image {
		width: 100%;
		height: 700upx;
	}
	.good image{
		width: 40upx; height: 40upx;
	}
	/* 第四小部分 */
	.maybelike{
		margin-bottom:90upx ;
	}
	.mltitle {
		font-size: 36upx;
		line-height: 90upx;
		margin-top: 10upx;
		color: #373A3F;
		text-indent: 20upx;
	}

	.recson {
		display: inline-block;
		width: 48%;
		margin: 0px 1%;
	}

	.recimg {
		width: 100%;
	}

	.recimg image {
		width: 100%;
		height: 320upx;
	}

	.rectit {
		color: #383B40;
		line-height: 70upx;
		font-size: 30upx;
		text-overflow:
			ellipsis;
		overflow: hidden;
		white-space: nowrap;
	}

	.recind {
		font-size: 26upx;
		color: #6E747B;
		text-overflow: ellipsis;
		overflow: hidden;
		white-space: nowrap;
	}

	.recpri {
		color: #BA545E;
		font-size: 24upx;
		vertical-align: top;
		margin: 10upx 0px;
	}

	.min_price {
		font-size: 34upx;
		vertical-align: middle;
	}

	.min_oprice {
		font-size: 28upx;
		color: #6E747B;
		vertical-align: middle;
		margin: 0px 10upx;
		text-decoration: line-through;
	}

	.addshopcar{display: flex; position: fixed; bottom: 0px; width: 100%;  font-size: 28upx;}
	.collect,.shopcar{width: 25%; text-align: center; background-color: white; color: #434343;}
	.addsc{width: 50%; text-align: center; background-color: #FD6801; color: white; line-height: 90upx;}
	.img image{width:40upx; height: 40upx;}
	.show {display: block;}
</style>
