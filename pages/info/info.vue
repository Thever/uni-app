<template>
	<view class="content">
		<view class="title">{{title}}...</view>
		<view class="art-content">
			<!-- nodes支持array和string -->
			<rich-text class="richText" :nodes="strings"></rich-text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title:'',
				strings: ''
			}
		},
		//	页面载入成功获取传入的参数
		onLoad(e) {
			console.log(e)
			uni.showLoading({
				title:'加载中...'
			})
			uni.request({
				url: 'https://unidemo.dcloud.net.cn/api/news/36kr/'+e.newsid,
				method: 'GET',
				data: {},
				success: res => {
					console.log(res)
					this.title = res.data.title
					this.strings = res.data.content
					uni.hideLoading()
				},
				fail: () => {},
				complete: () => {}
			});
		},
		methods: {
			
		}
	}
</script>

<style>
	.content{
		padding:10rpx 2%;
		width:96%;
		flex-wrap: wrap;
	}
	.title{
		line-height:2em;
		font-weight:700;
		font-size:38rpx;
	}
	.art-content{
		line-height:2rem;
	}
</style>
