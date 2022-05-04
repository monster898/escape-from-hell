<template>
	<view class="container">
		<view v-for="item,index in itemList">
			<Leaveitem :item="item" :key="index"></Leaveitem>
		</view>
		<u-empty :show="!itemListLength" text="暂无数据" mode="list" class="empty"></u-empty>
		<u-button class="leave_button" type="primary" @click="buttonClick">请假</u-button>
	</view>
</template>

<script>
	import Leaveitem from "../../component/Leaveitem.vue"
	export default {
		components:{ Leaveitem },
		data() {
			return {
				itemList:[]
			}
		},
		computed:{
			itemListLength(){
				return this.itemList.length
			}
		},
		onShow(){
			const applyInformation = uni.getStorageSync("apply_information")
			if(applyInformation){
				this.itemList = applyInformation
			}
		},
		methods: {
			buttonClick(){
				uni.navigateTo({
					url:"/pages/studentCenter/applyLeave"
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
.container {
	width: 100vw;
	min-height: 100vh;
	position: relative;
	background-color: rgb(247,247,247);
	.leave_button {
		position: fixed;
		bottom: 0;
		width: 750rpx;
	}
	.empty {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%,-50%);
	}
}
</style>
