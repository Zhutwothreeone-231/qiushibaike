<template>
	<view class="uni-list list-pd">
	    <view class="uni-list-cell cell-pd">
	        <view class="uni-uploader">
	            <view class="uni-uploader-head">
	                <view class="uni-uploader-title">点击可预览选好的图片</view>
	                <view class="uni-uploader-info">{{imageList.length}}/9</view>
	            </view>
	            <view class="uni-uploader-body">
	                <view class="uni-uploader__files">
	                    <block v-for="(image,index) in imageList" :key="index">
	                        <view class="uni-uploader__file">
								<view class="deleteImg icon iconfont icon-shanchu" @tap="deleteImg(index)"></view>
	                            <image class="uni-uploader__img" :src="image" :data-src="image" @tap="previewImage"></image>
	                        </view>
	                    </block>
	                    <view class="uni-uploader__input-box">
	                        <view class="uni-uploader__input" @tap="chooseImage"></view>
	                    </view>
	                </view>
	            </view>
	        </view>
	    </view>
	</view>
</template>

<script>
	var sourceType = [
	    ['camera'],
	    ['album'],
	    ['camera', 'album']
	]
	var sizeType = [
	    ['compressed'],
	    ['original'],
	    ['compressed', 'original']
	]
	export default {
		data(){
			return{
				title: 'choose/previewImage',
				imageList: [],
				sourceTypeIndex: 2,
				sourceType: ['拍照', '相册', '拍照或相册'],
				sizeTypeIndex: 2,
				sizeType: ['压缩', '原图', '压缩或原图'],
				countIndex: 8,
				count: [1, 2, 3, 4, 5, 6, 7, 8, 9]
			}
		},
		methods:{
			//上传图片的方法
			chooseImage: async function() {
							if (this.imageList.length === 9) { return; }
							uni.chooseImage({
								sourceType: sourceType[this.sourceTypeIndex],
								sizeType: sizeType[this.sizeTypeIndex],
								count: this.imageList.length + this.count[this.countIndex] > 9 ? 9 - this.imageList.length : this.count[this.countIndex],
								success: (res) => {
									this.imageList = this.imageList.concat(res.tempFilePaths);
									this.$emit('uploud',this.imageList)
								}
							})
						},
			previewImage: function(e) {
				var current = e.target.dataset.src
				uni.previewImage({
					current: current,
					urls: this.imageList
				})
			},
			deleteImg(index){
				uni.showModal({
					title: '提示',
					content: '是否要删除该图片',
					success: (res)=> {
						if (res.confirm) {
							this.imageList.splice(index,1);
							this.$emit('uploud',this.imageList)
						}
					}
				})
			}
		}
	}
</script>

<style>
	.uni-uploader__file{
		position: relative;
	}
	.deleteImg{
		position: absolute;
		z-index: 99;
		top: 0;
		right: 0;
		font-size: 16px;
		background: #333333;
		color: #FFFFFF;
		padding: 2upx 10upx;
		border-radius:10upx;
	}
</style>
