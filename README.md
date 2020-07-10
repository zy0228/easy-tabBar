# easy-tabBar (小程序版)
*为什么要写这个小组件： 在插件市场看了好多个都感觉不是很方便用起来，不是很复杂就是有bug。所以~*
___
## 配置:
| props            | type    | require | explain                               |
| ---------------- | ------- | ------- | ------------------------------------- |
| data             | Array   | true    | 数据源                             |
| value            | Number  | false   | 当前选中的值                    |
| inline           | Boolean | false   | 是否显示下边线                 |
| showSlider       | Boolean | false   | 是否显示下部slider条           |
| useTransition    | Boolean | false   | 使用过渡动画                    |
| useContentSlider | Boolean | false   | 是否使用相对于tab文字内容宽度的slider |

### 需要注意的地方
+ data的格式：
```
 data: [
    {
   	label: 'Home',
	icon: 'cubeic-home',
	value: 0
    }, {
    	label: 'Home',
	icon: 'cubeic-home',
	value: 1
    }
 ]
```
props中的value值要在data的范围内

+ 设置useContentSlider要保证showSlider为true, 默认的slider的宽度为tab的宽度，如果遇到某些场景需要展示的是相对于tab文字内容的宽度的话，那么useContentSlider设置为true即可。
+ 我只是提供了一个思路而已，你可以完全下载下来后自己魔改。喜欢的可以去上面的git址点个star~

# easy-scroll-Bar (小程序版)
*这个版本其实是来源于下面一个评论的需求。如果你用过头条，scroll-bar其实就是头条顶部bar的效果。用法很简单，像easy-tab-bar一样1s配置爽起来(componts/easy-scroll-bar)*
___
## 配置:
| props        | type   | require | explain |
| ------------ | ------ | ------- | ------- |
| usedTxts     | Array  | true    | 数据源 |
| currentIndex | Number | false   | 当前值 |

这个没什么好说的直接爽起来，同样的你也可以在我的基础上自己魔改~

最后，如果喜欢的话github地址（https://github.com/zy0228/easy-tabBar）点个赞吧
