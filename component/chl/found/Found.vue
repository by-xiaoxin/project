<template>
	<view class="found">
		<!-- 未找到商品组件和推荐 -->
		<scroll-view scroll-y="true" :style="'height:'+windowHeight+'px;'" >
			<view>
				<view class="found-shopping">
					未找到商品
				</view>
				<view class="mian">
					<shoppingBom></shoppingBom>
				</view>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	import shoppingBom from "../../lj/classifyShopping/shoppingBom/shoppingBom"
	export default{
		data(){
			return{
				windowHeight:0
			}
		},
		created() {
			this.windowHeight = uni.getSystemInfoSync().windowHeight-80//获取屏幕高度
		},
		components:{
			shoppingBom
		}
	}
</script>

<style scoped>
	.found{
		width: 100%;
	}
	
	.found-shopping{
		border: solid 1px red;
		width: 80%;
		height: 80upx;
		line-height: 80upx;
		margin: 80px auto 80upx;
		text-align: center;
	}
	
	.mian{
		background-color: #EEEEEE;
	}
	
	.mian-title{
		text-align: center;
		color: red;
		width: 100%;
		line-height: 100upx;
	}
</style>
