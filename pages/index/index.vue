<template>
	<view class="content">
		<view class="title">easy-tab-bar</view>
		<view class="tab-wrapper">
			<easy-tab-bar
				ref="tabBar"
				:data="tab"
				:value="currentValue"
				@tabClick="tabClick"
			>
			</easy-tab-bar>
		</view>
		<view class="tab-swiper">
			<swiper
				duration="200"
				:current="currentIndex"
				@change="change"
				easing-function="linear"
			>
				<swiper-item
					v-for="item in swiper"
					:style="{ backgroundColor: item.background }"
					:key="item.label"
				>
					<text>{{ item.name }}</text>
				</swiper-item>
			</swiper>
		</view>
		<view class="title">easy-scroll-bar</view>
		<easy-scroll-bar
			@scrollTabClick="scrollTabClick"
			:currentIndex="current"
			:usedTxt="text"
			ref="scrollTab"
		>
		</easy-scroll-bar>
		<view class="easy-scroll-tab-panel">{{innerContent}}</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			tab: [
				{
					label: 'Home',
					icon: 'cubeic-home',
					value: 0
				},
				{
					label: 'Like',
					icon: 'cubeic-like',
					value: 1
				},
				{
					label: 'Vip',
					icon: 'cubeic-vip',
					value: 2
				},
				{
					label: 'Me',
					icon: 'cubeic-person',
					value: 3
				}
			],
			swiper: [
				{
					name: 'Home',
					background: 'black'
				},
				{
					name: 'Like',
					background: 'yellow'
				},
				{
					name: 'Vip',
					background: 'blue'
				},
				{
					name: 'Me',
					background: 'pink'
				}
			],
			currentValue: 0,
			currentIndex: 0,
			current: 0,
			innerContent: '热点',
			text: ['热点', '直播', '图片', '科技', '娱乐', '游戏', '体育', '军事', '时尚', '养生', '									历史', '财经', '搞笑', '国际', '旅游']
		};
	},
	methods: {
		tabClick(value) {
			this.currentValue = Number(value);
			this.currentIndex = Number(value);
		},
		change(e) {
			this.currentValue = Number(e.detail.current);
		},
		scrollTabClick(index) {
			this.current = Number(index)
			this.innerContent = this.text[index]
		}
	}
};
</script>

<style>
.content {
	position: fixed;
	left: 0;
	right: 0;
	top: 0;
	bottom: 0;
	width: 100%;
	margin: 0;
}

.tab-wrapper {
	width: 100%;
	height: 40px;
}
.tab-swiper {
	height: calc(100% - 500px);
}

swiper {
	height: 100%;
	text-align: center;
}

swiper-item {
	display: flex;
	align-items: center;
	justify-content: center;
	color: #ffffff;
	font-size: 24px;
	font-weight: bold;
}

.title {
	font-size: 18px;
	margin-top: 20px;
	margin-bottom: 10px;
	border-bottom: 1px solid #111;
}

.easy-scroll-tab-panel {
	position: relative;
	background-color: #333333;
	width: 100%;
	height: 300px;
	color: #ffffff;
	font-size: 24px;
	font-weight: bold;
	display: flex;
	justify-content: center;
	align-items: center;
}
</style>
