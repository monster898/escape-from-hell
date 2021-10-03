<template>
	<view class="content">
		<view class="wrap">
				<u-swiper :list="list"></u-swiper>
		</view>
		<view class="personal_info" @click="navigateToStudentCenter">
			<view class="personal_info_container">
			<view class="personal_profile_container">
<!-- 				<view class="personal_info_profile"></view>	 -->
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
		<view class="button_center_container">
			<view class="teacher_center" @click="navigateToStudentCenter">
				<view class="teacher_center_icon"><image class="svg" src="https://cdn.haochen.me/teacher.svg"></image></view>
				<view class="teacher_center_text">教师中心</view>
			</view>
			<view class="student_center" @click="navigateToStudentCenter">
				<view class="student_center_icon"><image class="svg" src="https://cdn.haochen.me/ios-person.svg"></image></view>
				<view class="student_center_text">学生中心</view>
			</view>
		</view>
		<view class="collage_news">南工头条</view>
		<view class="collage_news_container">
			<li><a href="https://mp.weixin.qq.com/s/NwpxX8kfnZ4V8ou8yK9AEg">纪念九 · 一八活动</a><u-icon name="arrow-right" color="#CCCCCC" size="50"></u-icon></li>
			<li><a href="https://mp.weixin.qq.com/s/utvdb4EgwDS0RChf5ZIddg">收藏！一次说清新冠疫情期间,消毒与个人</a><u-icon name="arrow-right" color="#CCCCCC" size="50"></u-icon></li>
			<li><a href="https://mp.weixin.qq.com/s/tW8UGG_CXSKofG8BuynMMQ">关于全校大学生做好新冠肺炎疫情防控的紧</a><u-icon name="arrow-right" color="#CCCCCC" size="50"></u-icon></li>
			<li><a href="https://mp.weixin.qq.com/s/-dTvech_sg1e1BwNrLLTUg">八一建军节</a><u-icon name="arrow-right" color="#CCCCCC" size="50"></u-icon></li>
			<li><a href="https://mp.weixin.qq.com/s/a6NgbcI_9L-Gb913bjrMyg">关于收看征兵公益宣传片的通知</a><u-icon name="arrow-right" color="#CCCCCC" size="50"></u-icon></li>
			<li><a href="https://mp.weixin.qq.com/s/yVI7pzcQ2DGE8037SLED1w">"河"你一起，共度"南"关</a><u-icon name="arrow-right" color="#CCCCCC" size="50"></u-icon></li>
			<li><a href="https://mp.weixin.qq.com/s/2Uto_fiZOIgF4XZ_v1lUBA">2021年暑假致同学们的一封信</a><u-icon name="arrow-right" color="#CCCCCC" size="50"></u-icon></li>
			<li><a href="https://mp.weixin.qq.com/s/v5IBjaLJvgagCOXi9l4Aaw">习近平总书记在七一勋章颁授仪式上的讲话</a><u-icon name="arrow-right" color="#CCCCCC" size="50"></u-icon></li>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list:["https://cdn.haochen.me/indexImg.jpg"
				],
				src:"https://cdn.haochen.me/avatar1-modified.png"
			}
		},
		onLoad() {

		},
		methods: {
			navigateToStudentCenter(e){
				uni.navigateTo({
					url:"/pages/studentCenter/student_center"
					// success: res => {},
					// fail: () => {},
					// complete: () => {}
				})
			}
		}
	}
</script>

<style lang="scss">
	svg {
		color: #1296db
	}
	.content {
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
	.button_center_container {
		margin-top: 20rpx;
		width: 750rpx;
		height: 200rpx;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		background-color: rgb(255,255,255);
		.teacher_center {
			height: 200rpx;
			width: 100rpx;
			display: flex;
			flex-direction: column;
			justify-content: center;
			position: absolute;
			left: 187.5rpx;
			.svg {
				height: 100rpx;
				width: 100rpx;
				background-color: #469ef5;
				border-radius: 50%;
			}
			&_text {
				font-size:25rpx;
			}
		}
		.student_center {
			height: 200rpx;
			width: 100rpx;
			display: flex;
			flex-direction: column;
			justify-content: center;
			position: absolute;
			right: 187.5rpx;
			.svg {
				height: 100rpx;
				width: 100rpx;
				background-color: #59bb4e;
				border-radius: 50%;
			}
			&_text {
				font-size:25rpx
			}
		}
	}
	.collage_news {
		color: rgb(158,158,158);
		position: relative;
		right: 245rpx;
		margin-top:40rpx;
	}
	.collage_news_container {
		li {
			display: flex;
			flex-direction: row;
			align-items: center;
			justify-content: space-between;
			list-style: none;
			width: 750rpx;
			height: 100rpx;
			margin-top: 2rpx;
			background-color: rgb(255,255,255);
			a {
				margin-left: 67rpx;
				width: 570rpx;
				overflow-x: hidden;
				display: inline;
				white-space: nowrap;
				text-decoration: none;
			}
			a,a:link,a:visited,a:hover,a:active{
			    text-decoration: none;
			    color:inherit;
			}
		}
	}
</style>
