<template>
	<view class="personal_information_container">
		<li class="avatar_container"><view>头像</view><u-avatar @click="changeAvatar" class="avatar" :disabled="disableInput" :src="user_info.src" size="100" mode="circle"></u-avatar></li>
		<li class="department_container">
			<u-input v-model="user_info.department" placeholder="请输入院系" :disabled="disableInput" maxlength="30"  :custom-style="department_style" :clearable="false"></u-input>
			<view class="department_container_right">
				<u-field v-model="user_info.department_class" :disabled="disableInput" placeholder="请输入班级" maxlength="30" input-align="right" :field-style="class_position" :clearable="false"></u-field>
				<u-field v-model="user_information.major" :disabled="disableInput" input-align="right" placeholder="请输入专业"  :field-style="department_position" :clearable="false"></u-field>
			</view>
		</li>
		<li><view>学号</view><view class="form_style"><u-field  :disabled="disableInput" v-model="user_info.id" type="number" input-align="right" :field-style="field_style" maxlength="10" placeholder="请输入学号" :clearable="false"></u-field></view></li>
		<li><view>姓名</view><view class="form_style"><u-field  :disabled="disableInput" v-model="user_info.name" type="text" input-align="right" :field-style="field_style" maxlength="18" placeholder="请输入姓名" :clearable="false"></u-field></view></li>
		<li><view>性别</view><view class="form_style"><u-field  :disabled="disableInput" v-model="user_info.gender" type="text" input-align="right" :field-style="field_style" maxlength="4" placeholder="请输入性别" :clearable="false"></u-field></view></li>
		<li><view>民族</view><view class="form_style"><u-field  :disabled="disableInput" v-model="user_info.nation"  maxlength="10" :field-style="field_style" input-align="right" type="text" placeholder="请输入民族" :clearable="false"></u-field></view></li>
		<li><view>宿舍</view><view class="form_style"><u-field  :disabled="disableInput" v-model="user_info.dorm" maxlength="30" type="text" input-align="right" :field-style="field_style" placeholder="19号宿舍楼 # 888" :clearable="false"></u-field></view></li>
		<li><view>手机号</view><view class="form_style"><u-field :disabled="disableInput" v-model="user_info.phone_number" maxlength="11" input-align="right" :field-style="field_style" type="number" placeholder="13666666666" :clearable="false"></u-field></view></li>
		<li><view>备用手机号</view><view class="form_style"><u-field  :disabled="disableInput" v-model="user_info.second_phone_number" maxlength="11" input-align="right" :field-style="field_style" type="number" placeholder="13666666666" :clearable="false"></u-field></view></li>
		<li><view>QQ号</view><view class="form_style"><u-field
			type="number"
			v-model="user_info.QQ"
			placeholder="请输入备用QQ号"
			input-align="right"
			maxlength="11"
			:clearable="false"
			:field-style="field_style"
			:disabled="disableInput"
		></u-field></view></li>
		<li><view>Email</view><view class="form_style"><u-field type="text" :disabled="disableInput" v-model="user_info.email" input-align="right" :field-style="field_style" placeholder="请输入备用个人邮箱" maxlength="30" :clearable="false">请输入备用个人邮箱</u-field></view></li>
		<li><view>家长</view><view class="form_style"><u-field v-model="user_info.parent" :disabled="disableInput" type="text" input-align="right" :field-style="field_style" placeholder="请输入家长姓名" maxlength="16" :clearable="false"></u-field></view></li>
		<li><view>家长手机号</view><view class="form_style"><u-field v-model="user_info.parent_phone" :disabled="disableInput" input-align="right" :field-style="field_style" type="number" placeholder="13888888888" maxlength="11" :clearable="false"></u-field></view></li>
		<view class="button" v-if="showButton"><u-button type="primary" @click="buttonClick">修改</u-button></view>
		<u-modal v-model="showModal" :content="content" :title="modalTitle" @confirm="confirm" :show-cancel-button="true" @cancel="cancel" confirm-text="允许" cancel-text="不允许"></u-modal>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				user_info: {
					department:"",
					major:"",
					department_class:"",
					id:"2125185734",
					name:"王小飞",
					src:"http://kfn-order.oss-cn-shanghai.aliyuncs.com/2022/04/22/152ba3240276481cb0013f14b8b5e944.png",
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
				department_style: {
					fontSize: "30rpx"
				},
				showButton:false,
				showModal: false,
				modalTitle:"隐私提示",
				content:"是否允许小程序使用您输入的个人信息(仅用作显示并只储存在本地)？",
				disableInput: false
			};
		},
		onLoad() {
			const userInfo = uni.getStorageSync("user_info")
			if(userInfo){
				this.user_info = userInfo
			}
		},
		onShow() {
			const isAllowed = uni.getStorageSync("isAllowed")
			if(!isAllowed){
				this.showModal = true
			}else {
				this.showButton = true
			}
		},
		methods:{
			confirm(){
				uni.setStorageSync("isAllowed", true)
				this.showButton = true
			},
			cancel(){
				this.disableInput = true
			},
			buttonClick(){
				uni.setStorageSync("user_info", this.user_info)
				
				uni.showToast({
					icon:"success",
					title:"修改成功"
				})
				setTimeout(() => {
					uni.navigateBack()
				},1000)
			},
			changeAvatar(){
				if(!this.disableInput){
					uni.chooseImage({
						count:1,
						sourceType:["album"],
						success: (res) => {
							uni.saveFile({
								tempFilePath: res.tempFilePaths[0],
								success: (result) => {
									this.user_info.src = result.savedFilePath;
								},
								fail() {
									uni.showToast({
										icon: "error",
										title: "上传失败"
									})
								}
							});
						}
					})
				}
				
			}
		}
	}
</script>

<style lang="scss" scoped>
	.personal_information_container{
		overflow-x: hidden;
		background-color: rgb(247,247,247);
		position: absolute;
		width: 750rpx;
		height: 100%;
		li {
			font-size: 30rpx;
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
