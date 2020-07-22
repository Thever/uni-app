<template>
	<view class="content">
		<view class="uni-list">
			<!-- :data-newsid 用于地址动态传参数 newsid -->
			<view class="uni-list-cell" hover-class="uni-list-cell-hover" v-for="(item, index) in news" :key="index" @tap="openInfo" :data-newsid="item.post_id">
				<view class="uni-media-list">
					<image class="uni-media-list-logo" :src="item.author_avatar"></image>
					<view class="uni-media-list-body">
						<view class="uni-media-list-text-top">{{item.title}}</view>
						<view class="uni-media-list-text-bottom uni-ellipsis">{{item.created_at}}</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				news: []
			}
		},
		onLoad() {
			uni.showLoading({
				title:'加载中...'
			})
			uni.request({
				url: 'https://unidemo.dcloud.net.cn/api/news',
				method: 'GET',
				data: {},
				success: res => {
					this.news = res.data
					uni.hideLoading()
				},
				fail: () => {},
				complete: () => {}
			});
		},
		methods: {
			openInfo (e) {
				//	通过自定义data传入来获取参数，当然你也可以直接传入必要内容
				const newsid = e.currentTarget.dataset.newsid
				console.error(newsid)
				uni.navigateTo({
					//	通过地址栏动态传参
					url: '../info/info?newsid='+newsid,
					success: res => {},
					fail: () => {},
					complete: () => {}
				});
			}
		}
	}
</script>

<style>
	.uni-media-list-body{height: auto;}
	.uni-media-list-text-top{line-height:1.6em;}
</style>
