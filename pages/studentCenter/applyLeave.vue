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
		<view class="line"></view>
		<view class="height_1 padding">
			<view>辅导员姓名</view>
			<view class="arrow_right_2">
				<u-input v-model="teacher_name" type="text" placeholder="请输入" :clearable="false" :customStyle="custom_style_2" :placeholderStyle="placeholderStyle"/>
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
			:clearable="false"
		>
		</u-input></view>
		<view class="line"></view>
		<view class="height_1 padding"><view>是否告知家长</view><u-switch v-model="isTellParents"></u-switch></view>
		<view class="line"></view>
		<view class="height_1 padding"><view>是否离校</view><u-switch v-model="isLeaveSchool"></u-switch></view>
		<view class="line" v-if="isLeaveSchool"></view>
		<view class="height_1 padding" v-if="isLeaveSchool">
			<view>联系人姓名</view>
			<view class="arrow_right_2">
				<u-input v-model="em_name" type="text"  :clearable="false" placeholder="请输入紧急联系人姓名"/>
			</view>
		</view>
		<view class="line" v-if="isLeaveSchool"></view>
		<view class="height_1 padding" v-if="isLeaveSchool">
			<view>联系人电话</view>
			<view class="arrow_right_2">
				<u-input v-model="em_phone" type="text" :clearable="false"  placeholder="请输入紧急联系人电话"/>
			</view>
		</view>
		<view class="padding clearfix">
			<view>上传附件</view>
			<image src="http://kfn-order.oss-cn-shanghai.aliyuncs.com/2022/04/22/19b35c90de1548efbfdeb94236a0f3f3.svg">
		</view>
		<u-button class="apply_button" type="primary" @click="buttonClick">提交</u-button>
	</view>
	<u-select v-model="type_show" :list="list" mode="single-column" @confirm="confirmType"></u-select>
	<u-picker v-model="start_time_show" mode="time" :params="params" @confirm="confirmStart"></u-picker>
	<u-picker v-model="end_time_show" mode="time" :params="params" @confirm="confirmEnd"></u-picker>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				em_name:"",
				em_phone:"",
				isTellParents:false,
				isLeaveSchool:false,
				leave_type:"事假",
				start_time:"请选择",
				startTime:"",
				endTime:"",
				end_time:"请选择",
				apply_reason:"",
				teacher_name:"",
				placeholderStyle: "fontSize:32rpx",
				custom_style: {
					marginTop:"2rpx",
					paddingLeft:"25rpx",
					backgroundColor:"rgb(255,255,255)",
					width:"750rpx",
					fontSize:"32rpx"
				},
				custom_style_2: {
					// position:"absolute",
					width:"100rpx"
				},
				height:130,
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
			confirmType(data){
				this.leave_type = data[0].value;
			},
			confirmStart(data){
				this.start_time = `${data.year}-${data.month}-${data.day}`+" " + `${data.hour}:${data.minute}`;
				this.ios_start_time = `${data.year}/${data.month}/${data.day}`+" " + `${data.hour}:${data.minute}`;
				this.start_time_normal = `${data.month}-${data.day}`;
				this.startTime = this.start_time_normal;
			},
			confirmEnd(data){
				this.end_time = `${data.year}-${data.month}-${data.day}`+" " + `${data.hour}:${data.minute}`;
				this.ios_end_time = `${data.year}/${data.month}/${data.day}`+" " + `${data.hour}:${data.minute}`;
				this.end_time_normal = `${data.month}-${data.day}`;
				this.endTime = this.end_time_normal;
			},
			buttonClick(){
				if(this.start_time==="请选择"||this.end_time==="请选择"||this.apply_reason==="" || this.teacher_name === "" ||  (this.isLeaveSchool === true && this.em_name === "") || ( this.isLeaveSchool === true && this.em_phone === "")){
					uni.showToast({
						icon:"error",
						title:"请完善信息"
					})
					return;
				}
				let apply_time = new Date();
				let apply_time_temp = Date.now();
				apply_time = `${apply_time.getFullYear()}-${Number(apply_time.getMonth()) + 1 < 10 ? `0${Number(apply_time.getMonth()) + 1}`: Number(apply_time.getMonth()) + 1}-${apply_time.getDate() < 10 ? `0${apply_time.getDate()}` : apply_time.getDate()}` + " " + `${apply_time.getHours() < 10 ? `0${apply_time.getHours()}`: apply_time.getHours()}:${apply_time.getMinutes()< 10 ? `0${apply_time.getMinutes()}`: apply_time.getMinutes()}:${apply_time.getSeconds() < 10 ? `0${apply_time.getSeconds()}`: apply_time.getSeconds()}`;
				let continueDay = Math.floor((new Date(this.ios_end_time) - new Date(this.ios_start_time))/(1000*60*60*24));
				let continueHour = Math.floor(((new Date(this.ios_end_time) - new Date(this.ios_start_time))%(1000*60*60*24))/(1000*60*60));
				let data = {
					leave_type:this.leave_type,
					start_time:this.start_time,
					startTime:this.startTime,
					end_time:this.end_time,
					endTime:this.endTime,
					apply_reason:this.apply_reason,
					isTellParents:this.isTellParents,
					isLeaveSchool:this.isLeaveSchool,
					teacher_name:this.teacher_name,
					continueDay,
					continueHour,
					status:"审批通过",
					em_phone:this.em_phone,
					em_name: this.em_name,
					apply_time,
					apply_time_temp,
				};
				let applyInformation = uni.getStorageSync("apply_information")
				if(applyInformation){
					applyInformation.push(data)
				}else {
					applyInformation = [data]
				}
				uni.setStorageSync("apply_information",applyInformation)
				uni.showToast({
					icon:"success",
					title: "请假成功"
				})
				setTimeout(() => {
					uni.navigateBack()
				},1000)
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
		margin-bottom: 1px;
	}
	.apply_container {
		background-color: rgb(255,255,255);
		.apply_button {
			position: fixed;
			bottom: 0;
			right: 0;
			left: 0;
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
	.arrow_right_2 {
		position: relative;
	}
</style>
