<template>
	<view class="container">
	<view class="apply_container">
		<view class="height_1 padding" @click="type_show = true">
			<view>请假类型</view>
			<view class="arrow_right">
				{{leave_type}}
				<u-icon name="arrow-right" color="#CCCCCC" size="35"></u-icon>
			</view>
			
		</view>
		<view class="line"></view>
		<view class="height_1 padding" @click="start_time_show = true">
			<view>开始时间</view>
			<view class="arrow_right">
				{{start_time}}
				<u-icon name="arrow-right" color="#CCCCCC" size="35"></u-icon>
			</view>
		</view>
		<view class="line"></view>
		<view class="height_1 padding" @click="end_time_show = true">
			<view>结束时间</view>
			<view class="arrow_right">
				{{end_time}}
				<u-icon name="arrow-right" color="#CCCCCC" size="35"></u-icon>
			</view>
		</view>
		<view class="height_2 padding">
			请假原因
		</view>
		<view class="line"></view>
		<view class="reason_container">
		<u-input
			v-model="apply_reason"
			type="textarea"
			placeholder="请输入请假原因  (必填)"
			:height="height"
			:customStyle="custom_style"
		>
		</u-input></view>
		<view class="line"></view>
		<view class="height_1 padding"><view>是否告知家长</view><u-switch v-model="isTellParents"></u-switch></view>
		<view class="line"></view>
		<view class="height_1 padding"><view>是否离校</view><u-switch v-model="isLeaveSchool"></u-switch></view>
		<view class="padding clearfix">
			<view>上传附件</view>
			<image src="https://cdn.haochen.me/upload.svg">
		</view>
		<u-button class="apply_button" type="primary" @click="buttonClick">提交</u-button>
	</view>
	<u-select v-model="type_show" :list="list" mode="single-column"></u-select>
	<u-picker v-model="start_time_show" mode="time" :params="params" @confirm="confirmStart"></u-picker>
	<u-picker v-model="end_time_show" mode="time" :params="params" @confirm="confirmEnd"></u-picker>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				isTellParents:false,
				isLeaveSchool:false,
				leave_type:"事假",
				start_time:"请选择",
				startTime:"",
				endTime:"",
				end_time:"请选择",
				apply_reason:"",
				custom_style: {
					marginTop:"2rpx",
					paddingLeft:"25rpx",
					backgroundColor:"rgb(255,255,255)",
					width:"750rpx"
				},
				height:200,
				type_show: false,
				start_time_show: false,
				end_time_show: false,
				list: [
					{
						value: '事假',
						label: '事假'
					},
					{
					    value: '病假',
						label: '病假'
					},
					{
						value: '其他',
						label: '其他'
					}
				],
				params: {
					year: true,
					month: true,
					day: true,
					hour: true,
					minute: true,
				}
			}
		},
		methods: {
			confirmStart(data){
				this.start_time = `${data.year}-${data.month}-${data.day}`+" " + `${data.hour}:${data.minute}`;
				this.start_time_normal = `${data.year}-${data.month}-${data.day}`;
				this.startTime = this.start_time;
			},
			confirmEnd(data){
				this.end_time = `${data.year}-${data.month}-${data.day}`+" " + `${data.hour}:${data.minute}`;
				this.end_time_normal = `${data.year}-${data.month}-${data.day}`;
				this.endTime = this.end_time;
			},
			buttonClick(){
				if(this.start_time==="请选择"||this.end_time==="请选择"||this.apply_reason===""){
					uni.showToast({
						icon:"error",
						title:"请完善信息"
					})
					return;
				}
				let continueDay = (new Date(this.end_time_normal) - new Date(this.start_time_normal))/(1000*60*60*24);
				console.log(continueDay);
				let data = JSON.stringify([{
					leave_type:this.leave_type,
					start_time:this.start_time,
					startTime:this.startTime,
					end_time:this.end_time,
					endTime:this.endTime,
					apply_reason:this.apply_reason,
					isTellParents:this.isTellParents,
					isLeaveSchool:this.isLeaveSchool,
					continueDay
				}])
				let data2 = {
					leave_type:this.leave_type,
					start_time:this.start_time,
					startTime:this.startTime,
					end_time:this.end_time,
					endTime:this.endTime,
					apply_reason:this.apply_reason,
					isTellParents:this.isTellParents,
					isLeaveSchool:this.isLeaveSchool,
					continueDay
				};
				uni.getStorage({
					key:"apply_information",
					fail: function(res){
							uni.setStorage({
							key:"apply_information",
							data,
							success: function(){
							uni.showToast({
							icon:"success",
							title:"提交成功"
									})
								}
							})
						},
					success:function(){
								uni.getStorage({
								key:"apply_information",
								success: function (res){
									data = JSON.parse(res.data);
									console.log(data);
									data.push(data2);
									uni.setStorage({
										key:"apply_information",
										data,
										success: function (){
											uni.showToast({
												icon:"success",
												title:"提交成功"
											})
										}
									})
								}
							})
						}
					
				})
				
				
			},
		}
	}
</script>

<style lang="scss" scoped>
	.container {
		position: absolute;
		height: 100%;
		width: 750rpx;
		background-color: rgb(247,247,247);
	}
	.apply_container {
		background-color: rgb(255,255,255);
		.apply_button {
			position: absolute;
			bottom: 0;
			width: 750rpx;
		}
	}
	.height_1 {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		height: 120rpx;
	}
	.height_2 {
		display: flex;
		align-items: center;
		height: 100rpx;
	}
	.padding {
		margin-top: 2rpx;
		padding-left: 25rpx;
		padding-right: 30rpx;
		background-color: rgb(255,255,255);
	}
	image {
		float:left;
		width: 150rpx;
		height: 150rpx;
		padding-top: 30rpx;
		padding-left: 30rpx;
	}
	.reason_container {
		position: relative;
		background-color:"rgb(255,255,255)"
	}
	.clearfix:after {
		content:"";
		display: table;
		clear: both;
	}
	.line {
      border: 0;
      height: 0;
      // margin-top: 2rpx;
	  margin-left: 20rpx;
	  margin-right: 35rpx;
      border-top: 2rpx solid rgb(247,247,247);
    }
	.arrow_right {
		color: rgb(128,128,128);
	}
</style>
