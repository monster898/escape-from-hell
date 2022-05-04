<template>
	<view class="content">
		<view class="profile" @click="navigateToPersonalInformation">
			<u-avatar class="profile__avatar" :src="user_info.src" size="120" mode="circle"></u-avatar>
			<view class="profile__info">
				<view>
					<text class="profile__name">{{ user_info.name }}</text>
					<text class="profile__department">{{ user_info.department }}</text>
				</view>
				<view>
					<view class="profile__class"><i class="iconfont profile__class__icon">&#xe71e;</i><text>{{ user_info.department_class }}</text></view>
				</view>
			</view>
			<u-icon name="arrow-right" class="arrow_right" color="#CCCCCC" size="25"></u-icon>
		</view>
		
		<view class="card">
			<text class="card__text">常用工具</text>
			<view class="items">
				<view @click="navigateToLeaveList">
					<view class="item yellow">
						<i class="iconfont">&#xe617;</i>
					</view>
					<text>请销假</text>
				</view>
				
				<view @click="navigateToLeaveList">
					<view class="item red">
						<i class="iconfont" style="font-size: 30px;">&#xe79f;</i>
					</view>
					<text>健康晨报</text>
				</view>
				
				<view @click="navigateToLeaveList">
					<view class="item cyan">
						<i class="iconfont">&#xeac5;</i>
					</view>
					<text>健康日报</text>
				</view>
				
				<view @click="navigateToLeaveList">
					<view class="item orange">
						<i class="iconfont">&#xe6e5;</i>
					</view>
					<text>离返校登记</text>
				</view>
			</view>
		</view>
		<view class="card">
			<text class="card__text">学习日常</text>
			<view class="items">
				<view @click="navigateToLeaveList">
					<view class="item green">
						<i class="iconfont">&#xe600;</i>
					</view>
					<text>通知公告</text>
				</view>
				
				<view @click="navigateToLeaveList">
					<view class="item blue">
						<i class="iconfont" style="font-size: 30px;">&#xe6c9;</i>
					</view>
					<text>课堂缺勤记录</text>
				</view>
				
				<view @click="navigateToLeaveList">
					<view class="item purple">
						<i class="iconfont">&#xe601;</i>
					</view>
					<text>课堂评价</text>
				</view>
			</view>
		</view>
		
		<view class="card">
			<text class="card__text">其他</text>
			<view class="items">
				<view @click="navigateToLeaveList">
					<view class="item pink">
						<i class="iconfont" style="font-size: 30px;">&#xe646;</i>
					</view>
					<text>使用帮助</text>
				</view>
				
				<view @click="navigateToLeaveList">
					<view class="item cyan_dark">
						<i class="iconfont" style="font-size: 30px;">&#xe694;</i>
					</view>
					<text>返校申请</text>
				</view>
				
				<view @click="navigateToLeaveList">
					<view class="item blue_dark">
						<i class="iconfont" style="font-size: 30px;">&#xe84a;</i>
					</view>
					<text>问题反馈</text>
				</view>
			</view>
		</view>
		<view class="background"></view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				user_info:{
					src:"http://kfn-order.oss-cn-shanghai.aliyuncs.com/2022/04/22/152ba3240276481cb0013f14b8b5e944.png",
					name:"王小飞",
					department:"体育学院",
					department_class:"21电子三班"
				}
			};
		},
		// onLoad() {
		// 	// get user information
		// 	this.getUserInfo()
		// },
		onShow(){
			this.getUserInfo()
		},
		methods:{
			navigateToPersonalInformation(){
				uni.navigateTo({
					url:"/pages/studentCenter/personalInformation"
				})
			},
			navigateToLeaveList(){
				uni.navigateTo({
					url:"/pages/studentCenter/leave"
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

<style lang="scss" scoped>
.content {
	background-color: #f8f8f8;
	background-repeat: no-repeat;
	box-sizing: border-box;
	background-color: rgb(247,247,247);
	min-height: 100vh;
	padding-top: 50rpx;
	width: 100vw;
}

.background {
	width: 100%;
	position: absolute;
	top: 0;
	z-index: 2;
	height: 15%;
	text-align: center;
	color: #fff;
	background-image: linear-gradient(to bottom, #548cf7 0%, #7ab9f9 100%);
	clip-path: ellipse(100% 100% at 50% 0%);
	-webkit-clip-path: ellipse(100% 100% at 50% 0%);
}

.profile {
	z-index: 3;
	background-color: #FFFFFF;
	border-radius: 20rpx;
	display: flex;
	box-shadow: rgba(0, 0, 0, 0.1) 0px 1px 3px 0px, rgba(0, 0, 0, 0.06) 0px 1px 2px 0px;
	flex-direction: row;
	align-items: center;
	position: relative;
	margin-left: 25rpx;
	margin-right: 25rpx;
	padding: 30rpx;
	&__avatar {
		margin-top: 10rpx;
	}
	.arrow_right {
		position: absolute;
		right: 30rpx;
		top: 50%;
		transform: translateY(-50%);
	}
	&__info {
		display: flex;
		flex-direction: column;
		margin-left: 50rpx;
	}
	&__name {
		color: #404040;
		font-size: 38rpx;
	}
	&__department {
		font-size: 25rpx;
		margin-left: 15rpx;
		color: #4d4d4d;
	}
	&__class {
		font-size: 25rpx;
		height: 40rpx;
		background-color: #e4f2fb;
		color: #548cf7;
		border-radius: 15px;
		display: inline-block;
		position: relative;
		&__icon {
			margin-left: 27rpx;
			margin-right: 10rpx;
			color: #548cf7;
			font-size: 16px;
			position: absolute;
			top: 50%;
			transform: translateY(-50%);
		}
		text {
			margin-right: 30rpx;
			line-height: 40rpx;
			margin-left: 64rpx;
		}
	}
}


.card {
	background-color: #FFFFFF;
	border-radius: 10px;
	margin: 25rpx 25rpx 0 25rpx;
	padding-left: 25rpx;
	padding-right: 25rpx;
	box-shadow: rgba(0, 0, 0, 0.1) 0px 1px 3px 0px, rgba(0, 0, 0, 0.06) 0px 1px 2px 0px;
	&__text {
		color: #404040;
		font-size: 30rpx;
		display: inline-block;
		margin-top: 20rpx;
		margin-bottom: 20rpx;
	}
	.items {
		display: flex;
		flex-direction: row;
		gap: 80rpx;
		padding-bottom: 60rpx;
		.item {
			width: 100rpx;
			height: 100rpx;
			border-radius: 25%;
			.iconfont {
				font-size: 23px;
				color: #FFFFFF;
			}
			display: flex;
			align-items: center;
			justify-content: center;
		}
		> view {
			width: 100rpx;
			text-align: center;
			> text {
				font-size: 25rpx;
				color: rgb(128,128,128);
			}
		}
	}
	
}

.yellow {
	background-color: #f7d678;
}

.red {
	background-color: #f0a597;
}

.cyan {
	background-color: #8fe7c8;
}

.orange {
	background-color: #f4b87f;
}

.green {
	background-color: #c0e8aa;
}

.blue {
	background-color: #96b9f3;
}

.purple {
	background-color: #ccbced;
}

.pink {
	background-color: #e1b1e1;
}

.cyan_dark {
	background-color: #c4eb8c;
}

.blue_dark {
	background-color: #9aa2f8;
}

</style>
