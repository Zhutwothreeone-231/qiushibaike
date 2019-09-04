<template>
	<view>
		<!-- 自定义导航栏 -->
		<news-tab-bar :tabBars="tabBars" :tabIndex="tabIndex" @changeBar="changeBar"></news-tab-bar>
	</view>
</template>

<script>
	import newsTabBar from '../../components/news/news-tabbar.vue'
	export default {
		components: {
			newsTabBar
		},
		data() {
			return {
				tabIndex:0,
				tabBars: [{
					name: "关注",
					id: "guanzhu"
				}, {
					name: "话题",
					id: "huati"
				}]
			};
		},
		methods:{
			changeBar(index) {
				this.tabIndex=index
			}
		}
	}
</script>

<style>

</style>
