<template>
	<view class="content">
		<view class="wrap">
				<u-swiper :list="list"></u-swiper>
		</view>
		<view class="personal_info" @click="navigateToStudentCenter">
			<view class="personal_info_container">
					<u-avatar class="personal_profile_container" :src="user_info.src" size="75" mode="circle"></u-avatar>
				<view class="personal_info_infomation">
					<view class="personal_info_top">
						<view class="personal_info_username">{{ user_info.name }}</view>
						<view class="personal_info_department">{{user_info.department}}</view>
					</view>
					<view class="personal_info_bottom">
						<view class="personal_info_class">{{user_info.department_class}}</view>
					</view>
				</view>
				<u-icon name="arrow-right" class="arrow_right_top" color="#CCCCCC" size="35"></u-icon>
			</view>
		</view>
		<view class="button_center_container">
			<view class="teacher_center" @click="navigateToStudentCenter">
				<view class="teacher_center_icon"><view class="icon_background"><image class="svg" src="http://kfn-order.oss-cn-shanghai.aliyuncs.com/2022/04/22/c8ea58dd4ae0414f99ed11f3c4761607.svg"></image></view></view>
				<view class="teacher_center_text">教师中心</view>
			</view>
			<view class="student_center" @click="navigateToStudentCenter">
				<view class="student_center_icon"><view class="icon_background2"><image class="svg" src="http://kfn-order.oss-cn-shanghai.aliyuncs.com/2022/04/22/81f1ef9c512e455b89f8881c78967404.svg"></image></view></view>
				<view class="student_center_text">学生中心</view>
			</view>
		</view>
		<view>
			<view class="college_news">南工头条</view>
			<view class="college_news_container">
				<li><a>2022年应征入伍报名开始啦!</a><u-icon calss="arrow_right_bottom" name="arrow-right" color="#CCCCCC" size="35"></u-icon></li>
				<li><a>关于进行2021级新生思想状况及行为表现调查</a><u-icon name="arrow-right" calss="arrow_right_bottom" color="#CCCCCC" size="35"></u-icon></li>
				<li><a>新生代言人竞选</a><u-icon name="arrow-right" calss="arrow_right_bottom" color="#CCCCCC" size="35"></u-icon></li>
				<li><a>南阳理工学院第十三届大学生网络文化节</a><u-icon name="arrow-right" calss="arrow_right_bottom" color="#CCCCCC" size="35"></u-icon></li>
				<li><a>学党史国史，传承红色基因</a><u-icon name="arrow-right" calss="arrow_right_bottom" color="#CCCCCC" size="35"></u-icon></li>
				<li><a>我校两项活动入围河南省学生工作优秀成果</a><u-icon name="arrow-right" calss="arrow_right_bottom" color="#CCCCCC" size="35"></u-icon></li>
				<li><a>南工学生工作在线（极客壹佰）智慧学工研发</a><u-icon name="arrow-right" calss="arrow_right_bottom" color="#CCCCCC" size="35"></u-icon></li>
				<li><a>新生报道温馨提示!</a><u-icon name="arrow-right" calss="arrow_right_bottom" color="#CCCCCC" size="35"></u-icon></li>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list:["http://kfn-order.oss-cn-shanghai.aliyuncs.com/2022/04/22/0b0abecb3d254c8290633f81dd6702d9.jpg"],
				user_info:{
					name:"王小飞",
					department:"体育学院",
					department_class:"21电子三班",
					src:"http://kfn-order.oss-cn-shanghai.aliyuncs.com/2022/04/22/152ba3240276481cb0013f14b8b5e944.png",
				}
			}
		},
		onShow() {
			this.getUserInfo()
		},
		methods: {
			navigateToStudentCenter(e){
				uni.navigateTo({
					url:"/pages/studentCenter/student_center"
				})
			},
			getUserInfo(){
				const userInfo = uni.getStorageSync("user_info")
				if(userInfo){
					this.user_info = userInfo
				}
			}
		}
	}
</script>

<style lang="scss">
	svg {
		color: #1296db
	}
	.content {
		overflow-x: hidden;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		background-color: rgb(247,247,247);
	}
	.wrap {
		width: 750rpx;
	}
	.personal_info{
		margin-top: 20rpx;
		width: 750rpx;
		height: 130rpx;
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
		.personal_profile_container{
			margin-left: 25rpx;
			margin-top: 5rpx;
		}
		.personal_info_infomation {
			flex-basis: 70%;
			margin-left: 17rpx;
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
			font-size: 32rpx;
			margin-right: 10rpx;
			color: #404040;
		}
		.personal_info_department {
			font-size: 25rpx;
			color: #4d4d4d;
		}
		.personal_info_class {
			color: rgb(158,158,158);
			font-size: 25rpx;
			margin-top: 2rpx;
		}
		.arrow_right_top {
			position: relative;
			left: 20rpx;
			margin: auto;
		}
	}
	.button_center_container {
		margin-top: 20rpx;
		width: 750rpx;
		height: 200rpx;
		display: flex;
		flex-direction: row;
		gap: 280rpx;
		justify-content: center;
		align-items: center;
		background-color: rgb(255,255,255);
		.teacher_center {
			height: 200rpx;
			display: flex;
			flex-direction: column;
			justify-content: center;
			.svg {
				height: 50rpx;
				width: 50rpx;
			}
			&_text {
				color: #404040;
				margin-top: 5rpx;
				font-size: 26rpx;
			}
		}
		.student_center {
			height: 200rpx;
			display: flex;
			flex-direction: column;
			justify-content: center;
			.svg {
				height: 65rpx;
				width: 65rpx;
			}
			&_text {
				color: #404040;
				margin-top: 5rpx;
				font-size: 26rpx;
			}
		}
	}
	.college_news {
		color: rgb(128,128,128);
		margin-top: 40rpx;
		margin-left: 45rpx;
		margin-bottom: 15rpx;
		font-size: 28rpx;
	}
	.college_news_container {
		li {
			display: flex;
			flex-direction: row;
			align-items: center;
			justify-content: space-between;
			list-style: none;
			width: 750rpx;
			height: 100rpx;
			padding-right: 40rpx;
			color: #404040;
			margin-top: 2rpx;
			background-color: rgb(255,255,255);
			font-size: 32rpx;
			a {
				margin-left: 45rpx;
				width: 570rpx;
				overflow-x: hidden;
				display: inline;
				white-space: nowrap;
				text-decoration: none;
			}
			a,a:link,a:visited,a:hover,a:active{
			    text-decoration: none;
			    color: inherit;
			}
		}
	}
	.icon_background {
		width: 90rpx;
		height: 90rpx;
		background-color: #469ef5;
		display: flex;
		justify-content: center;
		align-items: center;
		border-radius: 50%;
		margin: auto;
	}
	.icon_background2{
		width: 90rpx;
		height: 90rpx;
		margin: auto;
		background-color: #59bb4e;
		display: flex;
		justify-content: center;
		align-items: center;
		border-radius: 50%;
	}
</style>
