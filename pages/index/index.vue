<template>
	<view class="indexContainer">
		<view class="header">
			<image src="/static/images/logo.png" class="logo"></image>
			<view class="search">
				<text class="iconfont icon-sousuo"></text>
				<input type="text" placeholder="搜索商品" placeholder-class="placeholder">
			</view>
			<button>重庆蔡徐坤</button>
		</view>
		<scroll-view scroll-x="true" enable-flex class="scrollContainer">
			<view class="scroolItem">
					<text :class="{active:currentIndex == -1}">推荐</text>
			</view>
			<view class="scroolItem" v-for="(item,index) in navData" :key='item.L1Id'>
				<text>推荐</text>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	import ajax from '../../API/ajax.js'
	export default {
		data() {
			return {
				navData:[],
				currentIndex:-1
			};
		},
		mounted() {
			this.getIndexData()
		},
		methods:{
			async getIndexData(){
				const result = await ajax('/getIndexData')
				this.navData = result.kingKongModule.kingKongList
			}
		}
	}
</script>

<style lang="less">
	.indexContainer{
		.header {
			display: flex;
			padding: 10rpx 0;
			.logo {
				width: 140rpx;
				height: 40rpx;
				margin: 10rpx 20rpx;
			}
			.search {
				position: relative;
				height: 60rpx;
				width: 420rpx;
				line-height: 60rpx;
				background-color: #eee;
				.iconfont {
					position: absolute;
					font-size: 35rpx;
					top: 5rpx;
					left: 5rpx;
				}
				input {
					height: 60rpx;
					width: 370rpx;
					margin-left: 50rpx;
				}
				.placeholder {
					font-size: 26rpx;
				}
			}
			button {
				width: 144rpx;
				height: 60rpx;
				text-align: center;
				line-height: 60rpx;
				font-size: 24rpx;
				padding: 0 4rpx;
				margin: 0 10rpx;
			}
		}
		.scrollContainer {
			display: flex;
			white-space: nowrap;
			.scroolItem {
				width: 140rpx;
				height: 100rpx;
				padding: 0 20rpx;
				& .active {
					border-bottom: 2rpx solid red;
				}
			}
		}
	}
</style>
