<template>
	<view class="content">
		<view class="personal_info" @click="navigateToPersonalInformation">
					<view class="personal_info_container">
					<view class="personal_profile_container">
						<u-avatar :src="src" size="75" mode="circle"></u-avatar>
					</view>
					<view class="personal_info_infomation">
					<view class="personal_info_top">
					<view class="personal_info_username">{{user_information.name}}</view>
					<view class="personal_info_department">{{user_information.department}}</view>
					</view>
					<view class="personal_info_bottom">
					<view class="personal_info_class">{{user_information.department_class}}</view>
					</view>
					</view>
					<u-icon name="arrow-right" class="arrow_right_top" color="#CCCCCC" size="35"></u-icon>
					</view>
		</view>
		<view class="item_container">
			<li @click="navigateToLeave"><image class="leave" src="https://cdn.haochen.me/leave.svg"><view class="item_text">请销假</view><u-icon name="arrow-right" color="#CCCCCC" size="35"></u-icon></li>
			<li @click="showToast"><image class="pencil" src="https://cdn.haochen.me/pencil.svg"><view class="item_text">健康晨报</view><u-icon name="arrow-right" color="#CCCCCC" size="35"></u-icon></li>
			<li @click="showToast"><image class="pencil" src="https://cdn.haochen.me/pencil.svg"><view class="item_text">健康日报</view><u-icon name="arrow-right" color="#CCCCCC" size="35"></u-icon></li>
			<li @click="showToast"><image class="add" src="https://cdn.haochen.me/add.svg"><view class="item_text">返校申请</view><u-icon name="arrow-right" color="#CCCCCC" size="35"></u-icon></li>
			<li @click="showToast"><image class="record" src="https://cdn.haochen.me/record.svg"><view class="item_text">离返校登记</view><u-icon name="arrow-right" color="#CCCCCC" size="35"></u-icon></li>
			<li @click="showToast"><image class="notification" src="https://cdn.haochen.me/notification.svg"></image><view class="item_text">通知公告</view><u-icon name="arrow-right" color="#CCCCCC" size="35"></u-icon></li>
			<li @click="showToast"><image class="record" src="https://cdn.haochen.me/record.svg"><view class="item_text">课堂缺勤记录</view><u-icon name="arrow-right" color="#CCCCCC" size="35"></u-icon></li>
			<li @click="showToast"><image class="record" src="https://cdn.haochen.me/record.svg"><view class="item_text">课堂评价</view><u-icon name="arrow-right" color="#CCCCCC" size="35"></u-icon></li>
			<li @click="showToast"><image class="help" src="https://cdn.haochen.me/help.svg"><view class="item_text">使用帮助</view><u-icon name="arrow-right" color="#CCCCCC" size="35"></u-icon></li>
		</view>
		<view>
			<u-toast ref="uToast" />
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				src:"https://cdn.haochen.me/avatar1-modified.png",
				user_information:{
					name:"王小飞",
					department:"电子工程",
					department_class:"21电子三班"
				}
			};
		},
		onShow() {
			var _this = this;
			console.log("load!");
			uni.getStorage({
				key:"user_information",
				success: function (res) {
					if(res.data == null){
						return;
					}else{
						_this.user_information = JSON.parse(res.data);
					}
				},
			});
			uni.getStorage({
				key:"src",
				success: function (res){
					if(res.data == null) {
						return;
					}else {
						_this.src = res.data;
					}
				}
			})
		},
		methods:{
			navigateToPersonalInformation(){
				uni.navigateTo({
					url:"/pages/studentCenter/personalInformation"
				})
			},
			navigateToLeave() {
				uni.navigateTo({
					url:"/pages/studentCenter/leave"
				})
			},
			showToast() {
				this.$refs.uToast.show({
					title: '待开发',
					type: 'warning',
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
			font-size: 30rpx;
			margin-right: 20rpx;
			font-weight: 440;
		}
		.personal_info_department {
			font-size: 25rpx;
		}
		.personal_info_class {
			color: rgb(128,128,128);
			font-size: 25rpx;
			margin-top: 2rpx;
		}
		.arrow_right_top {
			position: relative;
			left: 8rpx;
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
				left: 100rpx;
			}
			.record {
				width: 45rpx;
				height: 45rpx;
			}
			.leave {
				position: relative;
				top: 2rpx;
				width: 35rpx;
				height: 35rpx;
			}
			.pencil {
				position: relative;
				top: 5rpx;
				right: 10rpx;
				width: 50rpx;
				height: 50rpx;
			}
			.notification {
				width: 40rpx;
				height: 40rpx;
			}
			.help {
				width: 40rpx;
				height: 40rpx;
			}
			.add {
				width: 40rpx;
				height: 40rpx;
			}
		}
		
		margin-top: 20rpx;
	}
</style>
