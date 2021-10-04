<template>
	<view class="container">
		<view class="leave_item">
			<view class="leave_item_top">我的<text class="leave_item_type">事假</text>申请<text class="leave_item_startDay">06-14</text></view>
			<view class="leave_item_middle"><text class="leave_item_startTime">06-14 09:00</text><text class="zhi">至</text><text class="leave_item_endTime">06-15 06:00 </text>共(21) 小时</view>
			<view class="leave_item_bottom">已完成</view>
		</view>
		<view class="leave_item_arrow">
			<u-icon name="arrow-right" color="#CCCCCC" size="35"></u-icon>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style lang="scss" scoped>
.container {
	position: relative;
	display: flex;
	flex-direction: row;
	justify-content: space-between;
	align-items: center;
	width: 750rpx;
	height: 185rpx;
	background-color: rgb(255,255,255);
	.leave_item {
		display: flex;
		flex-direction: column;
		padding-left: 25rpx;
		.leave_item_type {
			margin-left: 10rpx;
			font-size: 35rpx;
		}
		.leave_item_top {
			color: #333333;
		}
		.leave_item_middle {
			margin-top: 15rpx;
			margin-bottom: 15rpx;
			color: rgb(128,128,128);
			font-size: 30rpx;
		}
		.leave_item_bottom {
			color: rgb(128,128,128);
			font-size: 30rpx;
		}
		.leave_item_startDay {
			position: absolute;
			right: 30rpx;
			color: rgb(128,128,128);
		}
		.zhi {
			margin-left: 10rpx;
			margin-right: 10rpx;
		}
	}
}
</style>