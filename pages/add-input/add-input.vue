<template>
	<view>
		<!-- 自定义导航栏 -->
		<uni-nav-bar :statusBar="true" rightText="发布" leftIcon="back" @click-left="back" @click-right="submit">
			<view class="u-f-ajc" @tap="lookChange">
				{{look}}
				<view class="icon iconfont icon-xialazhankai">

				</view>
			</view>
		</uni-nav-bar>
		<!-- 输入框 -->
		<view class="uni-textarea">
			<textarea v-model="text" value="" placeholder="请说出你想说的话" />
			</view>
		<!-- 上传多图 -->
		<upload-img @uploud="upload"></upload-img>
		<!-- 弹出层 -->
		<uni-popup :show="showFlag" position="middle" mode="fixed" @hidePopup="togglePopup">
			<view class="gonggao">
				<view class="u-f-ajc">
					<image src="../../static/common/addinput.png" mode="widthFix"></image>
				</view>
				<view>1.涉及黄色，政治，广告及骚扰信息</view>
				<view>2.涉及黄色，政治，广告及骚扰信息</view>
				<view>3.涉及黄色，政治，广告及骚扰信息</view>
				<view>4.涉及黄色，政治，广告及骚扰信息</view>
				<button type="default" @tap="togglePopup">朕知道了</button>
			</view>
		</uni-popup>
	</view>
</template>

<script>
	let lookArr=["所有人可见","仅自己可见"]
	import uniNavBar from '../../components/uni-nav-bar/uni-nav-bar.vue'
	import uploadImg from '../../components/common/uploadImg.vue'
	import uniPopup from '../../components/uni-popup/uni-popup.vue'
	export default {
		components: {
			uniNavBar,
			uploadImg,
			uniPopup
		},
		data() {
			return {
				look:"所有人可见",
				text:"",
				imgList:[],
				showFlag:true,
				isBack:false
			}
		},
		onBackPress() {
			// 如果没有写任何东西就直接返回
			if(!this.text && this.imgList.length<1) {
				return
			}
			//根据返回的提示的操作
			if(!this.isBack) {
				uni.showModal({
					content: '是否要保存为草稿？',
					cancelText: '不保存',
					confirmText: '保存',
					success: res => {
						if(res.confirm){
							console.log("保存")
						}else{
							console.log("不保存")
						}
						this.isBack=true;
						uni.navigateBack({
							delta: 1
						});
					},
				});
				return true
			}
			
		},
		methods: {
			// 返回按钮
			back() {
				uni.navigateBack({
					delta: 1
				})
			},
			//发布
			submit(){
				console.log("发布");
			},
			//隐私可见
			lookChange(){
				//注意this
				let me = this;
				uni.showActionSheet({
					itemList:lookArr,
					success(res) {
						me.look = lookArr[res.tapIndex];
					}
				})
			},
			upload(arr){
				this.imgList=arr
				console.log(this.imgList);
			},
			//隐藏弹出层
			togglePopup(){
				this.showFlag=false
			}
		}
	}
</script>

<style>
.uni-textarea{
	border: 1upx solid #EEEEEE;
}
.gonggao{
	width: 500upx;
}
.gonggao image{
	width: 75%;
	margin-bottom: 20upx;
}
.gonggao button{
	margin-top: 20upx;
	background: #FFE934;
	color: #171606;
}
</style>
