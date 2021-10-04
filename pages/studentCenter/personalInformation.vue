<template>
	<view class="personal_information_container">
		<li class="avatar_container"><view>头像</view><u-avatar @click="changeAvatar" class="avatar" :src="src" size="100" mode="circle"></u-avatar></li>
		<li class="department_container"><view>计算机与软件学院</view><view class="department_container_right"><u-field v-model="user_information.department_class" placeholder="请输入班级" maxlength="10" @input="isShowButton" input-align="right" :field-style="class_position"></u-field><u-field v-model="user_information.department" input-align="right" placeholder="请输入专业" @input="isShowButton" :field-style="department_position"></u-field></view></li>
		<li><view>学号</view><view class="form_style"><u-field @input="isShowButton" v-model="user_information.id" type="number" input-align="right" :field-style="field_style" maxlength="10" placeholder="请输入学号"></u-field></view></li>
		<li><view>姓名</view><view class="form_style"><u-field @input="isShowButton" v-model="user_information.name" type="text" input-align="right" :field-style="field_style" maxlength="3" placeholder="请输入姓名"></u-field></view></li>
		<li><view>性别</view><view class="form_style"><u-field @input="isShowButton" v-model="user_information.gender" type="text" input-align="right" :field-style="field_style" maxlength="1" placeholder="请输入性别"></u-field></view></li>
		<li><view>民族</view><view class="form_style"><u-field @input="isShowButton" v-model="user_information.nation"  maxlength="2" :field-style="field_style" input-align="right" type="text" placeholder="请输入民族"></u-field></view></li>
		<li><view>宿舍</view><view class="form_style"><u-field @input="isShowButton" v-model="user_information.dorm" maxlength="12" type="text" input-align="right" :field-style="field_style" placeholder="19号宿舍楼 # 888"></u-field></view></li>
		<li><view>手机号</view><view class="form_style"><u-field @input="isShowButton" v-model="user_information.phone_number" maxlength="11" input-align="right" :field-style="field_style" type="number" placeholder="13666666666"></u-field></view></li>
		<li><view>备用手机号</view><view class="form_style"><u-field @input="isShowButton" v-model="user_information.second_phone_number" maxlength="11" input-align="right" :field-style="field_style" type="number" placeholder="13666666666"></u-field></view></li>
		<li><view>QQ号</view><view class="form_style"><u-field
			type="number"
			v-model="user_information.QQ"
			placeholder="请输入备用QQ号"
			input-align="right"
			maxlength="11"
			:field-style="field_style"
			@input="isShowButton"
		></u-field></view></li>
		<li><view>Email</view><view class="form_style"><u-field type="text" @input="isShowButton" v-model="user_information.email" input-align="right" :field-style="field_style" placeholder="请输入备用个人邮箱" maxlength="15">请输入备用个人邮箱</u-field></view></li>
		<li><view>家长</view><view class="form_style"><u-field v-model="user_information.parent" @input="isShowButton" type="text" input-align="right" :field-style="field_style" placeholder="请输入家长姓名" maxlength="4"></u-field></view></li>
		<li><view>家长手机号</view><view class="form_style"><u-field v-model="user_information.parent_phone" @input="isShowButton" input-align="right" :field-style="field_style" type="number" placeholder="13888888888" maxlength="11"></u-field></view></li>
		<view class="button" v-if="showButton"><u-button type="primary" @click="buttonClick">修改</u-button></view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				src:"https://cdn.haochen.me/avatar1-modified.png",
				user_information: {
					department:"电子工程",
					department_class:"21电子三班",
					id:"2125185734",
					name:"王小飞",
					gender:"男",
					nation:"汉族",
					phone_number:"1366666666",
					second_phone_number:"13666666666",
					QQ:"88888",
					email:"888888@qq.com",
					parent:"王大拿",
					parent_phone:"13888888888",
					dorm:"19号宿舍楼 # 888",
				},
				field_style: {
					color: "rgb(128,128,128)",
					fontSize: "30rpx"
				},
				class_position: {
					position:"absolute",
					fontSize: "30rpx",
					right: "50rpx",
					top:"0rpx",
					color: "rgb(128,128,128)"
				},
				department_position : {
					position: "absolute",
					fontSize: "30rpx",
					right: "50rpx",
					top:"0rpx",
					color: "rgb(128,128,128)"
				},
				showButton:false
			};
		},
		onShow() {
			var _this = this;
			console.log("show!")
			uni.getStorage({
				key:"user_information",
				success: function (res) {
					if(res.data == null){
						return;
					}else{
						_this.user_information = JSON.parse(res.data);
					}
					
				},
			})
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
			isShowButton(){
				this.showButton = true;
			},
			buttonClick(){
				let data = JSON.stringify(this.user_information)
				uni.setStorage({
					key:"user_information",
					data
				})
				uni.showToast({
					icon:"success",
					title:"修改成功"
				})
			},
			changeAvatar(){
				var _this = this;
				uni.chooseImage({
					count:1,
					sizeType: ['original', 'compressed'],
					sourceType:["album"],
					success: function (res){
						uni.setStorage({
							key:"src",
							data:res.tempFilePaths[0]
						})
						_this.src = res.tempFilePaths[0]
					}
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.personal_information_container{
		background-color: rgb(247,247,247);
		position: absolute;
		height: 100%;
		li {
			position: relative;
			list-style: none;
			height: 100rpx;
			width: 750rpx;
			background-color: rgb(255,255,255);
			margin-top: 2rpx;
			padding: 0 20rpx 0 30rpx;
			display: flex;
			flex-direction: row;
			justify-content: space-between;
			align-items: center;
			.avatar {
				position: absolute;
				right:90rpx
			}
			.department_container_right {
				display: flex;
				flex-direction: column;
				// justify-content: center;
				position: absolute;
				right: 50rpx;
				color: rgb(158,158,158);
				.class{
					margin-bottom: 5rpx;
				}
			}
			// .infomation {
			// 	position: absolute;
			// 	right:80rpx;
			// 	color: rgb(158,158,158);
			// }
			// .id {
			// 	color: rgb(158,158,158);
			// 	position: absolute;
			// 	right: 0rpx;
			// 	width: 270rpx;
			// }
			// .name {
			// 	color: rgb(158,158,158);
			// 	position: absolute;
			// 	right: 0rpx;
			// 	width: 180rpx;
			// }
			// .gender {
			// 	color: rgb(158,158,158);
			// 	position: absolute;
			// 	right: 0rpx;
			// 	width: 120rpx;
			// }
			// .nation {
			// 	color: rgb(158,158,158);
			// 	position: absolute;
			// 	right: 0rpx;
			// 	width: 150rpx;
			// }
			// .dorm {
			// 	color: rgb(158,158,158);
			// 	position: absolute;
			// 	right: 0rpx;
			// 	width: 350rpx;
			// }
			// .phone_number {
			// 	color: rgb(158,158,158);
			// 	position: absolute;
			// 	right: 0rpx;
			// 	width: 300rpx;
			// }
			.form_style {
				position: absolute;
				right: 45rpx;
				color: red;
			}
		}
		.avatar_container {
			height: 150rpx;
		}
		.department_container {
			height: 150rpx;
		}
	}
	.button {
		width: 750rpx;
		margin-top: 15rpx;
	}
</style>
