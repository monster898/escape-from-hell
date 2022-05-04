<script>
	import {checkUpdateVersion} from "utils/common.js"
	export default {
		onLaunch: function() {
			console.log('App Launch')
			checkUpdateVersion()
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style lang="scss" scoped>
	/*每个页面公共css */
	@import "uview-ui/index.scss";
</style>
