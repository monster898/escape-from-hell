<template>
	<view class="container">
		<view v-for="item in itemList">
			<Leaveitem :item="item"></Leaveitem>
		</view>
		<u-button class="leave_button" type="primary" @click="buttonClick">请假</u-button>
	</view>
</template>

<script>
	import Leaveitem from "../../component/Leaveitem.vue"
	export default {
		components:{ Leaveitem },
		data() {
			return {
				id:1,
				itemList:[]
			}
		},
		onLoad() {
			console.log("load!");
		},
		onShow(){
			var _this = this;
			console.log("show");
			uni.getStorage({
				key:"apply_information",
				fail: function(){
					_this.itemList = [];
				},
				success: function(res){
					let data = JSON.parse(JSON.stringify(res.data));
					_this.itemList = JSON.parse(data);
					console.log(_this.itemList);
				}
			})
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
	position: absolute;
	background-color: rgb(247,247,247);
	.leave_button {
		position: fixed;
		bottom: 0;
		width: 750rpx;
	}
}
</style>
