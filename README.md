# easy-tabBar (小程序版)
### Basic example
```
<template>
	<easy-tab-bar
		ref="tabBar"
		:data="tab"
		:value="currentValue"
		@tabClick="tabClick"
	>
	</easy-tab-bar>
</template>

<script>
const TABDATA = [
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
]
export default {
	data() {
		tab: TABDATA,
		currentValue: 0
	},
	methods: {
		tabClick(value) {
			this.currentValue = Number(value);
		}
	}
}
</script>
```
---
### Motivation
*为什么要写这个小组件： 在插件市场看了好多个都感觉不是很方便用起来，不是很复杂就是有bug。所以~*
___
### Options:
| props            | type    | require | explain                               |
| ---------------- | ------- | ------- | ------------------------------------- |
| data             | Array   | true    | 数据源                             |
| value            | Number  | false   | 当前选中的值                    |
| inline           | Boolean | false   | 是否显示下边线                 |
| showSlider       | Boolean | false   | 是否显示下部slider条           |
| useTransition    | Boolean | false   | 使用过渡动画                    |
| useContentSlider | Boolean | false   | 是否使用相对于tab文字内容宽度的slider |
---
### Notice
+ data的格式：
```
 data: [
    {
			label: 'Home',
			icon: 'cubeic-home',
			value: 0  /** props中的value不能超出data中的value范围*/
    }, {
    	label: 'Home',
			icon: 'cubeic-home',
			value: 1
    }
 ]
```
+ 设置useContentSlider要保证showSlider为true, 默认的slider的宽度为tab的宽度，如果遇到某些场景需要展示的是相对于tab文字内容的宽度的话，那么useContentSlider设置为true即可。
+ 我只是提供了一个思路而已，你可以完全下载下来后自己魔改。喜欢的可以去上面的git址点个star~
---

# easy-scroll-Bar (小程序版)
### Basic example
```
<template>
	<easy-scroll-bar
		@scrollTabClick="scrollTabClick"
		:currentIndex="current"
		:usedTxt="text"
		ref="scrollTab"
	>
	</easy-scroll-bar>
</template>
<script>
export default {
	data() {
		return {
			current: 0,
			text: ['热点', '直播', '图片', '科技', '娱乐', '游戏', '体育', '军事', '时尚', '养生', '历史', '财经', '搞笑', '国际', '旅游']
		}
	},
	methods: {
		scrollTabClick(value) {
			this.current = Number(value)
		}
	}
}
</script>
```
---
### Motivation
*这个版本其实是来源于下面一个评论的需求。如果你用过头条，easy-scroll-bar其实就是头条顶部 bar的效果。用法很简单(组件所在componts/easy-scroll-bar)*
___

### Options
| props        | type   | require | explain |
| ------------ | ------ | ------- | ------- |
| usedTxts     | Array  | true    | 数据源 |
| margin     | Number  | false    | bar之间的间隔/默认10px |
| currentIndex | Number | false   | 当前值 |

这个没什么好说的直接爽起来，同样的你也可以在我的基础上自己魔改~

最后，如果喜欢的话github地址 https://github.com/zy0228/easy-tabBar 点个赞吧
