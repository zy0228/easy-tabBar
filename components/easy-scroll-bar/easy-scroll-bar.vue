<template>
	<view class="easy-scroll-nav-bar">
		<scroll-view scroll-x :scroll-left="scrollLeft">
			<view
				class="easy-scroll-nav-bar-item"
				v-for="(text, index) in usedTxts"
				:key="index"
				:data-index="index"
				:class="{ 'cube-scroll-nav-bar-item_active': currentIndex === index }"
				@click="clickHandler(index)"
				:style="{marginRight: margin+'px'}"
			>
				{{text}}
			</view>
		</scroll-view>
	</view>
</template>

<script>
/**
 * Easy Scroll Tabbar Component
 * @author Snoop Zhang (github: https://github.com/zy0228)
 * @property {Array} usedTxts 
 * @property {Number} currentIndex actived value
 * @property {Number} margin margin-right value
 */
const COMPONENT_NAME = 'easy-scroll-bar';
export default {
	name: COMPONENT_NAME,
	props: {
		usedTxts: {
			type: Array,
			default() {
				return ['热点', '直播', '图片', '科技', '娱乐', '游戏', '体育', '军事', '时尚', '养生', '历史', '财经', '搞笑', '国际', '旅游'];
			}
		},
		currentIndex: {
			type: Number,
			default: 0
		},
		margin: {
			type: Number,
			default: 10 // margin-right value unit/px
		}
	},
	data() {
		return {
			scrollLeft: 0
		};
	},
	mounted() {
		this.scrollerSize = 0
		const query = uni.createSelectorQuery().in(this);
		// set sorllTabEl and scrollTabSize
		query.selectAll('.easy-scroll-nav-bar-item').boundingClientRect(data => {
		  this.scrollTabBar = data
			for (let i = 0; i < data.length; i++ ) {
				this.scrollerSize += data[i].width
			}
		}).exec()
		// set viewportSize
		query.select('.easy-scroll-nav-bar').boundingClientRect(bound => {
			this.viewportSize = bound.width
		}).exec()
	},
	methods: {
		clickHandler(index) {
			if (!this.viewportSize || !this.scrollerSize) return
			const minTranslate = Math.min(0, this.viewportSize - this.scrollerSize)
			const middleTranslate  = this.viewportSize / 2
			let size = 0
			
			for(let i = 0; i < this.scrollTabBar.length; i++) {
				if (i === index) {
					size += this.scrollTabBar[i].width / 2
					break
				}
				size += (this.scrollTabBar[i].width + this.margin)
			}
			let translate = middleTranslate - size
			translate = Math.max(minTranslate, Math.min(0, translate))
			this.scrollLeft = translate < 0 ? Math.abs(translate) : translate
			this.$emit('scrollTabClick', index);
		}
	}
};
</script>

<style>
.easy-scroll-nav-bar {
	margin: 0;
	position: relative;
	display: flex;
	white-space: nowrap;
}

.easy-scroll-nav-bar-item {
	display: inline-block;
	vertical-align: top;
	padding: 15rpx 30rpx;
	z-index: 1;
	background-color: #f4f5f6;
}

.easy-scroll-nav-bar-item span {
	z-index: -1;
}

/**选中状态css**/
.cube-scroll-nav-bar-item_active {
	color: #f85959;
}
</style>
