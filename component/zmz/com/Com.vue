<template>
	<view :class="['main',show?'show':'']">
		<!-- 选择商品配置 -->
		<view :class="['cgoodsc',nums==1?'show ':'']">
			<view class="cgoodscon">
				<!-- 当前选择的内容 -->
				<view class="goodsinfc">
					<view class="googsleft">
						<image :src="datas.cover"></image>
					</view>
					<view class="goodsright">
						<view class="goodsprc">
							￥<text>{{datas.min_price}}</text>
						</view>
						<view class="goodsprcs">
							<text v-for="(item,index) in pick" :key="index">{{item.dcolor}}</text>
						</view>
					</view>
				</view>
				<!-- 可选内容 -->
				<view class="pickup" v-for="(item,index) in pick" :key="index">
					<view class="picktit">
						{{item.name}}
					</view>
					<view class="pickcon">
						<view @click="change(item,index,im,ind)" :class="['pickcson',im.key?'active':'']" v-for="(im,ind) in item.goodsSkusCardValue" :key="ind">
							{{im.value}}
						</view>
					</view>
				</view>
			</view>
			<view class="choicef">
				<view class="shopf">
					购买数量
				</view>
				<view class="addde">
					<text @click="del" :class="['nums',num<=1?'contorl':'']">-</text><text>{{num}}</text><text @click="add" class="nums">+</text>
				</view>
			</view>
			<view class="sure" @click="none">
				加入购物车
			</view>
		</view>
		<!-- 收货地址 -->
		<view :class="['harvestad',nums==2?'show ':'']">
			<view class="haad">
				收货地址
			</view>
			<view class="address">
				<image src="../../../static/zmz/img/position.png"></image>
			</view>
			<view class="sure" @click="lose">
				选着新的地址
			</view>
		</view>
		<!-- 服务说明 -->
		<view :class="['Serdes',nums==3?'show ':'']">
			<view class="Serdescon">
				<view class="haad">
					服务说明
				</view>
				<view class="mif">
					<view class="sgood">
						√
					</view>
					<view class="mi">
						仿米自营
					</view>
				</view>
				<view class="mif">
					<view class="sgood">
						√
					</view>
					<view class="mi">
						仿米发货
						<text>由仿米发货</text>
					</view>
				</view>
				<view class="mi">
					<view class="sgood">
						√
					</view>
					<view class="mi">
						七天无理由退货
					</view>
				</view>
				<view class="mif">
					<view class="sgood">
						√
					</view>
					<view class="mi">
						运费说明
						<text>不管满多少，就是不包邮；</text>
						<text>特殊产品也是一样；</text>
					</view>
				</view>
			</view>
			<view class="sure" @click="lose">
				确定
			</view>	
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				datas: {},
				pick: [],
				num:1,
				pickup:[]
			}
		},
		props:{
			show:{
				type : Boolean
			},
			nums:{
				type : Number
			},
			ids:{
				type : Number
			}
		},
		methods:{
			none:function(){
				this.$emit("nones",{show:false,datas:this.pickup,num:this.num})
			},
			lose:function(){
				this.$emit("lose",{show:false})
			},
			del:function(){
				if(this.num>1){
					this.num--;
				}else{
					this.num=1
				}
			},
			add:function(){
				this.num++;
			},
			change: function(item, index, im, ind) {
				this.pickup = []
				let actt = []; //key=true所在数组的下标
				let acttt = []; //key=false所在数组的下标
				let seft = []; //key=true所在数组的数据
				let seff = []; //key=false所在数组的数据
				this.pick[index].dcolor = im.value
				this.pick[index].goodsSkusCardValue.forEach((a, b) => {
					if (a.value.indexOf(im.value) >= 0) { //查找到所点击的对应数组
						a.key = true //将点击的按钮改为ture
						actt.push(b)
						seft.push(a)
					} else {
						a.key = false //将未点击的按钮改为false
						acttt.push(b)
						seff.push(a)
					}
				})
				for (var i = 0; i < actt.length; i++) {
					this.$set(this.pick[index].goodsSkusCardValue, actt[i], seft[i]) //往this.pick中重新赋值给对应的数组改变数据
				}
				for (var i = 0; i < acttt.length; i++) {
					this.$set(this.pick[index].goodsSkusCardValue, acttt[i], seff[i])
				}
				for (var i = 0; i < this.pick.length; i++) {
					this.pickup.push(this.pick[i].dcolor)
				}
			}
		},
		watch:{
			ids(){
				console.log("kldfhgkdf")
			}
		},
		mounted() {
			let _this = this
			// 指定商品详情
			let list = []
			uni.request({
				url: "http://ceshi3.dishait.cn/api/goods/"+_this.ids+"",
				success(res) {
					console.log(res.data.data)
					_this.datas = res.data.data
					_this.pick = _this.datas.goodsSkusCard
					for (var i = 0; i < _this.pick.length; i++) {
						for (var j = 0; j < _this.pick[i].goodsSkusCardValue.length; j++) {
							_this.pick[i].goodsSkusCardValue[j].key = false
						}
						_this.pick[i].goodsSkusCardValue[0].key = true
						list.push(_this.pick[i].goodsSkusCardValue[0].value)
					}
					for (var i = 0; i < list.length; i++) {
						_this.pick[i].dcolor = list[i]
						_this.pickup.push(list[i])
					}
				}
			})
		}
	}
</script>

<style scoped>
	/* 选择商品配置 */
	.main {
		position: fixed;
		top: 15vh;
		width: 100%;
		background-color: white;
		height: 85vh;
		display: none;
		border-radius: 10upx;
		z-index: 20;
	}
	
	.cgoodsc,.harvestad,.Serdes{display: none;}
	.cgoodscon {
		padding: 20upx;
	}
	
	.goodsinfc {
		display: flex;
	}
	
	.googsleft {
		width: 25%;
		display: inline-block;
		text-align: center;
		border-radius: 10px;
		border: 1px solid #E0E3E6;
		padding-top: 10upx;
	}
	
	.googsleft image {
		width: 80%;
		height: 150upx;
	}
	
	.goodsright {
		width: 70%;
		display: inline-block;
		padding-top: 30upx;
		margin-left: 20upx;
	}
	
	.goodsprc {
		color: #F86A07;
		font-size: 24upx;
		vertical-align: top;
	}
	
	.goodsprc text {
		font-size: 38upx;
		font-weight: bold;
		vertical-align: middle;
	}
	
	.goodsprcs text {
		font-size: 28upx;
		margin: 0px 10upx;
	}
	
	.picktit {
		line-height: 100upx;
		font-size: 32upx;
	}
	
	.pickcson {
		width: 30%;
		margin: 0px 2%;
		display: inline-block;
		background-color: #F8F9FB;
		border-radius: 10upx;
		line-height: 80upx;
		font-size: 32upx;
		text-align: center;
		border: 1px solid #F8F9FB;
	}
	
	.active {
		background-color: #FCE0D5;
		border: 1px solid #F76D0F;
	}
	
	.choicef {
		display: flex;
		height: 100upx;
		line-height: 100upx;
		width: 100%;
		position: absolute;
		padding-top: 10upx;
		margin-bottom: 10upx;
		border-top: 1px solid #F7F7F7;
		bottom: 80upx;
	}
	.shopf{width: 20%; font-size: 34upx;}
	.addde{width: 70%; display: inline-block; text-align: right; }
	.addde text{display: inline-block; width: 80upx; text-align: center; border: 1px solid #DBDBDD;
		height: 80upx; line-height: 80upx; font-size: 34upx;}
	.nums{background-color: #F8F8F8; font-weight: bold; }
	.contorl{font-weight: normal; color: #DBDBDD;}
	/* 收货地址 */
	.haad {
		text-align: center;
		font-size: 30upx;
		line-height: 80upx;
		border-bottom: 1px solid #F3F3F3;
		font-weight: bold;
	}
	
	.address {
		height: 100upx;
		border-bottom: 1px solid #F3F3F3;
	}
	.address image{width: 50upx; height: 50upx; margin: 20upx 0px;}
	.show {
		display: block;
	}
	
	/* 服务说明 */
	.mif{display: flex; margin: 40upx 0px;}
	.sgood{width: 10%; display: inline-block;margin: 0px 2%; width: 40upx; height: 40upx; background-color: #FD6801;
		border-radius: 50%; text-align: center; color: white;}
	.mi {
		width: 80%; display: inline-block;
		
		font-size: 30upx;
	}
	
	.mi text {
		display: block;
		font-size: 26upx;
		color: #D4D4D4;
		margin: 20upx 0px;
	}
	
	.sure {
		background-color: #FD6801;
		color: white;
		text-align: center;
		line-height: 80upx;
		position: absolute;
		bottom: 0px;
		width: 110%;
		left: -10%;
	}
	.addshopcar{display: flex; position: fixed; bottom: 0px; width: 100%;  font-size: 28upx;}
	.collect,.shopcar{width: 25%; text-align: center; background-color: white; color: #434343;}
	.addsc{width: 50%; text-align: center; background-color: #FD6801; color: white; line-height: 90upx;}
	.img image{width:40upx; height: 40upx;}
</style>
