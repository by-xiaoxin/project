<template>
	<view id="popup-select">
		<view class="mark" v-show="fixd">
		</view>
		<view class="popup" :class="[fixd?'.popup-options':'']">
			<!--整体容器  :style="'bottom:'+fixd+'upx;'"-->
			<view class="popup-select">
				<!-- 选项内容 -->
				<view class="popup-select-pic-price">
					<!-- 图片/价钱/选项配置 -->
					<view class="popup-pic">
						<image :src="selectCarListConfig.cover" mode=""></image>
					</view>
					<view class="popup-price">
						<view class="popup-price-cont">
							<text class="popup-price-cont-icon">￥</text>
							<text class="popup-price-cont-pri">3369</text>
						</view>
						<view class="popup-price-des">
							<text class="popup-price-des-color">123</text>
							<text class="popup-price-des-capa">456</text>
							<text class="popup-price-des-meal">789</text>
						</view>
					</view>
				</view><!-- 图片/价钱 -->

				<view class="popup-select-color" v-for="(item) in selectCarListConfig.goods_skus_card" :key="item.id">
					<!-- 颜色选项 -->
					<view class="popup-select-color-text">{{item.name}}</view>
					<view class="popup-select-color-option">
						<view class="option" v-for="(ite) in item.goods_skus_card_value" :key="ite.value">{{ite.value}}</view>
					</view>
				</view> <!-- 颜色选项 -->


				<view class="quantity">
					<!--购买数量 -->
					<view class="quantity-font">购买数量</view>
					<view class="quantity-num">
						<view class="miu">-</view>
						<view class="numvalue">12</view>
						<view class="plus">+</view>
					</view>
				</view>
				<!--购买数量 -->
			</view><!-- 选项内容 -->

			<view class="joincar" @click="handleJoinCar">
				加入购物车
				<!-- {{selectCarListConfig}} -->
			</view>
		</view>
		<!--整体容器 -->
	</view>
</template>

<script>
	export default {
		data() {
			return {

			}
		},
		props: {
			fixd: {
				type: Boolean
			},
			selectCarListConfig: {
				type: Object
			}
		},
		methods: {
			handleJoinCar() {
				console.log(this.$props.selectCarListConfig)
			}
		},
		created() {

		},
		onLoad() {

		}
	}
</script>

<style scoped>
	.popup.popup-options {
		//弹窗动画
		position: fixed;
		transition: all 0.5s;
		bottom: 0upx;
	}

	.mark {
		width: 100%;
		height: 100%;
		position: absolute;
		top: 0;
		z-index: 20;
		background: rgba(0, 0, 0, 0.6);
	}

	.popup {
		image {
			width: 100%;
			height: 100%;
		}

		position: fixed;
		transform: all 0.5s;
		bottom: -980upx;
		width: 100%;
		z-index: 100;
		background: white;
		border-radius: 20upx 20upx 0 0;

		& &-select {
			//选项内容
			width: 93%;
			margin: auto;

			&-pic-price {
				//价钱和已选配置
				display: flex;
				justify-content: space-between;
				margin: 30upx 0;
				padding: 20upx 0;

				.popup-pic {
					width: 27%;
					height: 190upx;
					padding: 20upx;
					border: 1px solid #ECEDF0;
					border-radius: 10upx;
				}

				.popup-price {
					width: 63%;
					line-height: 20upx;

					&-cont {
						margin: 90upx 0 25upx 0;

						&-icon {
							color: $background-text-color;
							font-size: 20upx;
						}

						&-pri {
							font : {
								size: 40upx;
								weight: 700;
							}

							color: $background-text-color;
						}
					}

					&-des {
						&-capa {
							margin: 0 10upx;
						}
					}
				}
			}

			&-color {
				&-text {
					height: 88upx;
					line-height: 88upx;
					text-indent: 1em;
				}

				&-option {
					display: flex;

					// justify-content: space-between;
					.option {
						margin-right: 30upx;
						border-radius: $uni-border-radius-base;
						padding: 10upx 80upx;
						background: $uni-bg-color-grey;
					}

					.active {
						border: 1px solid $background-text-color;
						background: lighten($background-text-color, 40%);
						color: $background-text-color;
					}
				}
			}

			.quantity {
				display: flex;
				justify-content: space-between;
				height: 80upx;
				line-height: 80upx;
				padding-top: 30upx;

				&-num {
					display: flex;

					view {
						width: 70upx;
						height: 70upx;
						line-height: 70upx;
						text-align: center;
						border: 1px solid lighten($uni-border-color, 10%);

						&:first-child {
							border-right: 0;
							border-radius: 6upx 0 0 6upx;
							background: $uni-bg-color-grey;
						}

						&:last-child {
							border-left: 0;
							border-radius: 0 6upx 6upx 0;
							background: $uni-bg-color-grey;
						}
					}
				}
			}
		}

		.joincar {
			//加入购物车
			text-align: center;
			padding: 30upx 0;
			background: $background-text-color;
			color: white;
		}
	}
</style>
