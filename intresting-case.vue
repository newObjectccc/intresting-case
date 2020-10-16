<template>
	<view class="entrust-content" :style="isSelecting?'position:fixed':''">
		<Header pageName="common">
			<view class="header-wrapper">
				<image class="head-img" src="/static/back.png" @tap="navBack"></image>
				<view class="wrap">
					<view :class="curEntrustType===1?'current':''" @tap="chooseCurrentType(1)">当前委托<span v-if="curEntrustType===1"></span></view>
					<view :class="curEntrustType===2?'current':''" @tap="chooseCurrentType(2)">历史委托<span v-if="curEntrustType===2"></span></view>
				</view>
			</view>
			<view class="nav-wrapper">
				<view class="nav" @tap="selectConditionFunc">所有币种<image src="/static/arrow.png"></image></view>
				<view class="nav" @tap="selectConditionFunc">委托类型<image src="/static/arrow.png"></image></view>
				<view class="nav" @tap="selectConditionFunc">买入卖出<image src="/static/arrow.png"></image></view>
				<view class="nav" v-if="curEntrustType===2" @tap="selectConditionFunc">全部状态<image src="/static/arrow.png"></image></view>
				<view v-if="isSelecting!==0" class="condition-content" :class="isSelecting?'show-content':'hide-content'">
					<view class="search-wrapper">
						<image class="search-img" src="/static/image/quotation/search.png"></image>
						<input :class="searchValue!==''?'focus-style':'search-input'" type="text" v-model="searchValue" placeholder="请输入币种名称" />
						<image v-if="searchValue!==''" class="search-img posi-right" src="/static/currency-transactions/close.png" @tap="clearInputValueFunc"></image>
					</view>
					<view class="content">
						<view class="left">
							<view class="condition-item" :class="curCoinCondition===index?'condition-item-active':''" v-for="(item,index) in coinCondition" :key="index" @tap="chooseCoinConditionFunc(index)">
								{{item}}
							</view>
						</view>
						<view class="right" @touchmove="touchMoveHandle">
							<view class="scroll">
								<view class="item" v-for="(item,index) in conditionResult" :key="index">
									<view class="left">
										{{item.mainCoin}}
										<span>/{{item.transferCoin}}</span>
									</view>
									<view class="right">
										{{item.value}}
									</view>
								</view>
							</view>
						</view>
					</view>
				</view>
				<view v-if="isSelecting!==0" :class="isSelecting?'show-cover':'hide-cover'" @tap="selectConditionFunc"></view>
			</view>
		</Header>
		<view class="padding-empty"></view>
		<view class="division-line"></view>
		<block v-for="(item,index) in [12,2,3,4,5]" :key="index">
			<OrderItem currentPage="entrust"></OrderItem>
		</block>
	</view>
</template>

<script>
	import OrderItem from '../components/order-item.vue'
	export default {
		components: {
			OrderItem
		},
		data() {
			return {
				curEntrustType: 1,
				searchValue: '',
				isSelecting: 0,
				coinCondition: ['所有币种','收藏','USDT','HUSD','BTC','ETH'],
				curCoinCondition: 0,
				conditionResult: [{
					mainCoin: 'BTC',
					transferCoin: 'USDT',
					value: '158129308.2736'
				},{
					mainCoin: 'BTC',
					transferCoin: 'USDT',
					value: '158129308.2736'
				},{
					mainCoin: 'BTC',
					transferCoin: 'USDT',
					value: '158129308.2736'
				},{
					mainCoin: 'BTC',
					transferCoin: 'USDT',
					value: '158129308.2736'
				},{
					mainCoin: 'BTC',
					transferCoin: 'USDT',
					value: '158129308.2736'
				},{
					mainCoin: 'BTC',
					transferCoin: 'USDT',
					value: '158129308.2736'
				},{
					mainCoin: 'BTC',
					transferCoin: 'USDT',
					value: '158129308.2736'
				},{
					mainCoin: 'BTC',
					transferCoin: 'USDT',
					value: '158129308.2736'
				},{
					mainCoin: 'BTC',
					transferCoin: 'USDT',
					value: '158129308.2736'
				},{
					mainCoin: 'BTC',
					transferCoin: 'USDT',
					value: '158129308.2736'
				},{
					mainCoin: 'BTC',
					transferCoin: 'USDT',
					value: '158129308.2736'
				},{
					mainCoin: 'BTC',
					transferCoin: 'USDT',
					value: '158129308.2736'
				},{
					mainCoin: 'BTC',
					transferCoin: 'USDT',
					value: '158129308.2736'
				},{
					mainCoin: 'BTC',
					transferCoin: 'USDT',
					value: '158129308.2736'
				},{
					mainCoin: 'BTC',
					transferCoin: 'USDT',
					value: '158129308.2736'
				}]
			}
		},
		methods: {
			chooseCurrentType(e) {
				this.curEntrustType = e
			},
			navBack() {
				uni.navigateBack({
					delta: 1
				})
			},
			selectConditionFunc() {
				this.isSelecting = !this.isSelecting
			},
			chooseCoinConditionFunc(e) {
				this.curCoinCondition = e
			},
			clearInputValueFunc() {
				this.searchValue = ''
			}
		}
	}
</script>

<style lang="scss" scoped>
	.entrust-content {
		width: 100%;
		.header-wrapper {
			@include frn;
			align-items: center;
			padding: 0 30rpx;
			height: 80rpx;
			.head-img {
				width: 18rpx;
				height: 34rpx;
				padding: 6rpx 30rpx 6rpx 0;
			}
			.wrap {
				flex: 1;
				@include frncc;
				justify-content: center;
				align-items: center;
				padding-right: 48rpx;
				view {
					padding: 0 31rpx;
					font-size: 29rpx;
					font-weight: 500;
					color: #333333;
					@include fcncc;
					position: relative;
					span {
						display: block;
						width: 54rpx;
						height: 7rpx;
						background: linear-gradient(90deg,#4b86f7, #3c69e9);
						position: absolute;
						bottom: -19rpx;
					}
				}
				.current {
					color: #538BF6;
				}
			}
		}
		.nav-wrapper {
			@include frn;
			align-items: center;
			justify-content: space-around;
			padding: 27rpx 0;
			height: 80rpx;
			position: relative;
			.nav {
				font-size: 25rpx;
				color: #888b99;
				@include frncc;
				image {
					width: 12rpx;
					height: 7rpx;
					margin-left: 9rpx;
				}
			}
			.condition-content {
				overflow: hidden;
				.search-wrapper {
					height: 63rpx;
					padding: 0 22rpx;
					background-color: #f6f7f9;
					border-radius: 9rpx;
					margin: 27rpx 18rpx;
					@include frncc;
					.focus-style {flex: 1;font-size: 24rpx;color: #999999;margin-left: 10rpx;}
					.search-img {width: 26rpx;height: 26rpx;}
					.posi-right {}
					.search-input {width: 200rpx;font-size: 24rpx;color: #999999;margin-left: 10rpx;}
				}
				.content {
					flex: 1;
					@include frn;
					height: 683rpx;
					.left {
						width: 236rpx;
						height: inherit;
						background-color: #F6F7F9;
						.condition-item {
							width: 236rpx;
							height: 83rpx;
							padding: 24rpx 0 24rpx 34rpx;
							font-size: 25rpx;
							text-align: left;
							color: #333333;
							&-active {
								color: #538bf6;
								background-color: #FFFFFF;
							}
						}
					}
					.right {
						flex: 1;
						height: inherit;
						overflow-y: scroll;
						position: relative;
						.scroll {
							width: 100%;
							height: inherit;
							position: absolute;
							top: 0;
							left: 0;
							.item {
								width: 100%;
								@include frn;
								align-items: center;
								justify-content: space-between;
								padding: 27rpx;
								.left {
									width: 180rpx;
									font-size: 27rpx;
									font-weight: 500;
									color: #333333;
									background-color: #FFFFFF;
									span {
										color: #666666;
										font-size: 22rpx;
										font-weight: 400;
									}
								}
								.right {
									flex: 1;
									text-align: right;
									font-size: 27rpx;
									color: #e34f68;
								}
							}
						}
					}
				}
			}
			.show-content {
				width: 100%;
				height: 800rpx;
				position: absolute;
				top: 80rpx;
				left: 0;
				background-color: #FFFFFF;
				animation: slider-down .3s ease-in-out forwards;
				z-index: 999;
				border-radius: 0 0 12rpx 12rpx;
			}
			.hide-content {
				width: 100%;
				height: 800rpx;
				position: absolute;
				top: 80rpx;
				left: 0;
				background-color: #FFFFFF;
				animation: slider-up .3s ease-in-out forwards;
				z-index: 999;
				border-radius: 0 0 12rpx 12rpx;
			}
			.show-cover {
				width: 100%;
				height: 100vh;
				position: absolute;
				left: 0;
				top: 80rpx;
				animation: cover-show .2s ease-in-out .3s forwards;
				z-index: 991;
			}
			.hide-cover {
				width: 100%;
				height: 100vh;
				position: absolute;
				left: 0;
				top: 80rpx;
				animation: cover-hide .3s ease-in-out forwards;
				z-index: 991;
			}
		}
		.padding-empty {
			width: 100%;
			height: 80rpx;
		}
	}
	@keyframes slider-down {
		0% {
			height: 0;
		}
		100% {
			height: 800rpx;
		}
	}
	@keyframes slider-up {
		0% {
			height: 800rpx;
		}
		100% {
			height: 0;
		}
	}
	@keyframes cover-show {
		0% {
			background-color: rgba(0,0,0,0);
		}
		100% {
			background-color: rgba(0,0,0,.4);
		}
	}
	@keyframes cover-hide {
		0% {
			background-color: rgba(0,0,0,.4);
		}
		100% {
			background-color: rgba(0,0,0,0);
		}
	}
</style>
