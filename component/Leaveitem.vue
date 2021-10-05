<template>
	<view class="leave_container" @click="handleClick">
		<view class="leave_item">
			<view class="leave_item_top">我的<text class="leave_item_type">{{item.leave_type}}</text>申请<text class="leave_item_startDay">{{item.startTime}}</text></view>
			<view class="leave_item_middle"><text class="leave_item_startTime">{{item.start_time}}</text><text class="zhi">至</text><text class="leave_item_endTime">{{item.end_time + " "}} </text>(共{{Number(item.continueDay) === 0 ? `${item.continueHour}小时`:`${item.continueDay}天${item.continueHour}小时`}})</view>
			<view class="leave_item_bottom" :class="{finish:isfinish}">{{item.status}}</view>
		</view>
		<view class="leave_item_arrow">
			<u-icon name="arrow-right" color="#CCCCCC" size="35"></u-icon>
		</view>
	</view>
</template>

<script>
	export default {
		name:"Leaveitem",
		props:["item","isfinish"],
		data() {
			return {
			}
		},
		methods: {
			handleClick(){
				uni.navigateTo({
					url:`/pages/studentCenter/leave_details?data=${JSON.stringify(this.item)}`
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
.leave_container {
	position: relative;
	display: flex;
	flex-direction: row;
	justify-content: space-between;
	align-items: center;
	width: 750rpx;
	height: 185rpx;
	margin-top: 2rpx;
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
			font-size: 20rpx
		}
		.leave_item_bottom {
			color: #008000;
			font-size: 28rpx;
		}
		.leave_item_startDay {
			position: absolute;
			right: 30rpx;
			color: rgb(128,128,128);
			font-size: 20rpx;
			top:30rpx;
		}
		.zhi {
			margin-left: 10rpx;
			margin-right: 10rpx;
		}
		.finish {
			color: rgb(128,128,128);
		}
	}
}
</style>