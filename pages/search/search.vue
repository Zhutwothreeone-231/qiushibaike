<template>
	<view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		},
		onNavigationBarButtonTap(e) {
			if(e.index==0) {
				uni.navigateBack({
					delta:1
				})
			}
		},
		onNavigationBarSearchInputChanged(e) {
			console.log(e.text);
		},
		onNavigationBarSearchInputConfirmed(e) {
			console.log(e.text);
		}
	}
</script>

<style>

</style>
