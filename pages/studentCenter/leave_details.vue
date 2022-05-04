<template>
	<view class="details_container">
		<view class="status">
			<view class="status_icon">
				<image src="http://kfn-order.oss-cn-shanghai.aliyuncs.com/2022/04/23/bbb906c13f2f4543b0774ba7ea556208.svg">
			</view>
			<view class="status_text">审批通过</view>
		</view>
		<view class="approval">审批情况</view>
		<view class="line"></view>
		<view class="flex teacher_approval">{{item.teacher_name}}审批<view class="teacher_approval_time">({{ randomTime }})</view></view>
		<view class="approval_reason">审批意见: 同意</view>
		<view class="approval_details">
			<view class="approval_details_front">请假详情</view>
			<view class="approval_details_end">申请时间{{item.apply_time}}</view>
		</view>
		<view class="line"></view>
		<view class="details">
			<view class="margin">开&nbsp;始&nbsp;请&nbsp;假&nbsp;时&nbsp;间&nbsp;: &nbsp;{{item.start_time}}</view>
			<view class="margin">请&nbsp;假&nbsp;结&nbsp;束&nbsp;时&nbsp;间&nbsp;: &nbsp;{{item.end_time}}<text class="day">{{item.continueDay}}天</text></view>
			<view class="margin letter_1">请&nbsp;&nbsp;&nbsp;假&nbsp;&nbsp;&nbsp;类&nbsp;&nbsp;&nbsp;型&nbsp;&nbsp;: &nbsp;{{item.leave_type}}</view>
			<view class="margin letter_1">请&nbsp;&nbsp;&nbsp;假&nbsp;&nbsp;&nbsp;原&nbsp;&nbsp;&nbsp;因&nbsp;&nbsp;: &nbsp;{{item.apply_reason}}</view>
			<view class="margin">已&nbsp;&nbsp;告&nbsp;&nbsp;知&nbsp;&nbsp;家&nbsp;&nbsp;长&nbsp;: &nbsp;{{item.isTellParents ? "是": "否"}}</view>
			<view class="margin">是&nbsp;否&nbsp;需&nbsp;要&nbsp;离&nbsp;校&nbsp;: &nbsp;{{item.isLeaveSchool ? "是" : "否"}}</view>
			<view class="margin" v-if="item.isLeaveSchool">紧&nbsp;&nbsp;急&nbsp;&nbsp;联&nbsp;&nbsp;系&nbsp;&nbsp;人 : &nbsp;{{item.em_name}}</view>
			<view class="margin letter" v-if="item.isLeaveSchool">紧急联系人电话&nbsp;: &nbsp;{{item.em_phone}}</view>
			<view class="margin">附件: 无</view>
		</view>
		<view class="button">
			<view class="button_left" @click ="handleLeftClick">我要续假</view>
			<view class="button_right" @click ="handleRightClick">我要销假</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				item:{},
				randomTime: ""
			}
		},
		onLoad: function (option){
			this.item = JSON.parse(option.data);
			let randomTime = Number(this.item.apply_time_temp) + (1000*60*15);
			let apply_time = new Date(randomTime);
			apply_time = `${apply_time.getFullYear()}-${Number(apply_time.getMonth()) + 1 < 10 ? `0${Number(apply_time.getMonth()) + 1}`: Number(apply_time.getMonth()) + 1}-${apply_time.getDate() < 10 ? `0${apply_time.getDate()}` : apply_time.getDate()}` + " " + `${apply_time.getHours() < 10 ? `0${apply_time.getHours()}`: apply_time.getHours()}:${apply_time.getMinutes()< 10 ? `0${apply_time.getMinutes()}`: apply_time.getMinutes()}`;
			this.randomTime = apply_time;
		},
		methods: {
			handleLeftClick(){
				uni.navigateTo({
					url:"/pages/studentCenter/applyLeave"
				})
			},
			handleRightClick(){
				const applyInformation = uni.getStorageSync("apply_information")
				applyInformation.forEach((item,index) => {
					if(item.apply_time_temp === this.item.apply_time_temp){
						applyInformation.splice(index,1)
					}
				})
				uni.setStorageSync("apply_information", applyInformation)
				uni.showToast({
					icon:"success",
					title:"销假成功"
				})
				setTimeout(() => {
					uni.navigateBack()
				},1000)
			}
		}
	}
</script>

<style lang="scss" scoped>
	.details_container {
		background-color: rgb(255,255,255);
		padding: 0 25rpx 0 25rpx;
		overflow-x: hidden;
	}
	.status {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		width: 750rpx;
		height: 415rpx;
		image {
			width: 180rpx;
			height: 180rpx;
		}
		&_text {
			margin-top: 30rpx;
			font-weight: 900;
			font-size: 35rpx;
			letter-spacing:1rpx
		}
	}
	.approval {
		font-size: 31rpx;
		// font-weight: bold;
		letter-spacing: 2rpx;
	}
	.line {
	  border: 0;
	  height: 0;
	  margin-top: 20rpx;
	  margin-bottom: 20rpx;
	  // margin-left: 20rpx;
	  // margin-right: 35rpx;
	  border-top: 2rpx solid rgb(247,247,247);
	}
	.teacher_approval {
		font-size: 30rpx;
		// font-weight: bold;
		letter-spacing: 2rpx;
		margin-bottom: 20rpx;
		&_time{
			margin-left: 10rpx;
			color: rgb(128,128,128);
			font-size: 25rpx;
			display: flex;
			align-items: center;
			font-weight: normal;
		}
	}
	.flex {
		display: flex;
	}
	.approval_reason {
		color: rgb(128,128,128);
		margin-bottom: 50rpx;
		font-size: 29rpx;
	}
	.approval_details {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		&_front {
			font-size: 31rpx;
			font-weight: bold;
			letter-spacing: 2rpx;
		}
		&_end {
			font-size: 25rpx;
			color: rgb(128,128,128);
		}
	}
	.details {
		margin-top: 25rpx;
	}
	.margin {
		margin: 25rpx 0 25rpx 0;
		color: #404040;
	}
	.day {
		display: inline-block;
		background-color: #418cff;
		border-radius: 20%;
		color: rgb(255,255,255);
		display: inline-flex;
		align-items: center;
		font-size: 30rpx;
		padding: 2rpx 10rpx 2rpx 8rpx;
		margin-left: 10rpx;
	}
	.letter {
		letter-spacing: 1rpx;
		&_1{
			letter-spacing: 1rpx;
		}
	}
	.button {
		display: flex;
		flex-direction: row;
		padding: 0 25rpx 0 25rpx;
		position: fixed;
		bottom: 25rpx;
		width: 750rpx;
	}
	.button_left {
		width: 42%;
		background-color: rgb(255,255,255);
		color: #418cff;
		display: flex;
		justify-content: center;
		align-items: center;
		border: 1rpx solid #418cff;
		height: 80rpx;
		border-radius: 15rpx;
		margin-left: -20rpx;
	}
	.button_right {
		width: 42%;
		background-color: #418cff;
		color: rgb(255,255,255);
		height: 80rpx;
		display: flex;
		justify-content: center;
		align-items: center;
		position: absolute;
		right: 100rpx;
		border-radius: 15rpx;
	}
</style>
