<template>
	<view class="container">
		<u-button class="leave_button" type="primary" @click="buttonClick">请假</u-button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
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
	position: absolute;
	background-color: rgb(247,247,247);
	.leave_button {
		position: fixed;
		bottom: 0;
		width: 750rpx;
	}
}
</style>
