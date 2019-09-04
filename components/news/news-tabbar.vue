<template>
	<view>
		<uni-nav-bar @click-right="openAdd">
			<!-- 左边 -->
			<template slot="left">
				<view class="nav-left">
					<view class="icon iconfont icon-qiandao">
		
					</view>
				</view>
			</template>
			<!-- 中间 -->
			<view class="nav-tab-bar u-f-ajc">
				<view class="" v-for="(item,index) in tabBars" :key="index" >
					<view class="u-f-ajc" :class="{'active':tabIndex==index}" @tap="changeBar(index)">
						{{item.name}}
					</view>
				</view>
			</view>
			<!-- 右边 -->
			<template slot="right">
				<view class="nav-right u-f-ajc">
					<view class="icon iconfont icon-bianji1"></view>
				</view>
			</template>
		</uni-nav-bar>
	</view>
</template>

<script>
	import uniNavBar from '../../components/uni-nav-bar/uni-nav-bar.vue'
	export default {
		components:{
			uniNavBar
		},
		props:{
			tabBars:Array,
			tabIndex:Number
		},
		methods:{
			changeBar(index) {
				this.$emit("changeBar",index)
			},
			openAdd(){
				uni.navigateTo({
					url:"../../pages/add-input/add-input"
				})
			}
		}
	}
</script>

<style>
	.nav-left>view,.nav-right>view{
		font-size: 40upx;
	}
	.nav-left>view{
		color: #FF9619;
	}
	.nav-left{
		margin-left: 16upx;
	}
	.nav-right{
		width: 100%;
	}
	.nav-tab-bar{
		width: 100%;
		margin-left: -20upx;
		position: relative;
	}
	.nav-tab-bar>view{
		font-size: 32upx;
		padding: 0 15upx;
		font-weight: bold;
		color: #969696;
	}
	.active{
		color: #333333!important;
	}
	.nav-tab-bar-line{
		border-bottom: 5upx solid #FEDE33;
		border-top: 5upx solid #FEDE33;
		width: 70upx;
		border-radius: 20upx;
		position: absolute;
		bottom: 12upx;
	}
</style>
