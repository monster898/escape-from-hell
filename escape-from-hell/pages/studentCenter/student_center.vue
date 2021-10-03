<template>
	<view class="content">
		<view class="personal_info" @click="navigateToPersonalInformation">
					<view class="personal_info_container">
					<view class="personal_profile_container">
						<u-avatar :src="src" size="75" mode="circle"></u-avatar>
					</view>
					<view class="personal_info_infomation">
					<view class="personal_info_top">
					<view class="personal_info_username">郭俊峰</view>
					<view class="personal_info_department">计算机与软件学院</view>
					</view>
					<view class="personal_info_bottom">
					<view class="personal_info_class">19智能三班</view>
					</view>
					</view>
					<u-icon name="arrow-right" color="#CCCCCC" size="50"></u-icon>
					</view>
		</view>
		<view class="item_container">
			<li><view class="item_icon"></view><view class="item_text">请销假</view><u-icon name="arrow-right" color="#CCCCCC" size="50"></u-icon></li>
			<li><view class="item_icon"></view><view class="item_text">健康晨报</view><u-icon name="arrow-right" color="#CCCCCC" size="50"></u-icon></li>
			<li><view class="item_icon"></view><view class="item_text">健康日报</view><u-icon name="arrow-right" color="#CCCCCC" size="50"></u-icon></li>
			<li><view class="item_icon"></view><view class="item_text">返校申请</view><u-icon name="arrow-right" color="#CCCCCC" size="50"></u-icon></li>
			<li><view class="item_icon"></view><view class="item_text">离返校登记</view><u-icon name="arrow-right" color="#CCCCCC" size="50"></u-icon></li>
			<li><view class="item_icon"></view><view class="item_text">通知公告</view><u-icon name="arrow-right" color="#CCCCCC" size="50"></u-icon></li>
			<li><view class="item_icon"></view><view class="item_text">课堂缺勤记录</view><u-icon name="arrow-right" color="#CCCCCC" size="50"></u-icon></li>
			<li><view class="item_icon"></view><view class="item_text">课堂评价</view><u-icon name="arrow-right" color="#CCCCCC" size="50"></u-icon></li>
			<li><view class="item_icon"></view><view class="item_text">使用帮助</view><u-icon name="arrow-right" color="#CCCCCC" size="50"></u-icon></li>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				src:"https://cdn.haochen.me/avatar1-modified.png"
			};
		},
		methods:{
			navigateToPersonalInformation(){
				uni.navigateTo({
					url:"/pages/studentCenter/personalInformation"
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.content {
		background-color: rgb(247,247,247);
		min-height: 100%;
		width: 750rpx;
		position: absolute;
	}
	.personal_info{
		width: 750rpx;
		height: 150rpx;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		background-color: rgb(255,255,255);
	}
	.personal_info_container {
		width: 750rpx;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		.personal_profile_container{
			flex-basis: 15%;
			display: flex;
			flex-direction: row;
			justify-content: center;
			align-items: center;
		}
		.personal_info_infomation {
			flex-basis: 70%;
		}
		.personal_info_information {
			display: flex;
			flex-direction: column;
		}
		.personal_info_top {
			display: flex;
			align-items: baseline;
			padding-bottom: 2rpx;
		}
		.personal_info_username {
			font-size: 40rpx;
			margin-right: 20rpx;
			font-weight: 520;
		}
		.personal_info_department {
			font-size: 25rpx;
		}
		.personal_info_class {
			color: rgb(158,158,158);
			font-size: 25rpx;
			margin-top: 2rpx;
		}
		// .personal_info_profile {
		// 	width: 75rpx;
		// 	height: 75rpx;
		// 	border-radius: 50%;
		// 	// background-color: red;
		// 	background: url("../../static/avatar1-modified.png") no-repeat center;
		// 	background-size: 37.5px;
		// }
	}
	.item_container {
		display: flex;
		flex-direction: column;
		justify-content: center;
		li {
			position: relative;
			list-style: none;
			height: 100rpx;
			width: 680rpx;
			background-color: rgb(255,255,255);
			display: flex;
			margin-top: 2rpx;
			justify-content: space-between;
			flex-direction: row;
			align-items: center;
			padding-left: 45rpx;
			padding-right: 25rpx;
			.item_text {
				position: absolute;
				left: 45rpx;
			}
		}
		
		margin-top: 20rpx;
	}
</style>
