<template>
  <view class="easy-tab-bar" :class="{'easy-tab-bar_inline': inline}">
    <easy-tab
      v-for="item in data"
      ref="easyTab"
      class="easy-tab"
      :label="item.label"
      :value="item.value"
      :key="item.label"
      :showCntSlider="useContentSlider"
    >
    </easy-tab>
    <view v-if="showSlider" :class="[showSliderCls, 'easy-tab-bar-slider']" :style="{width: sliderWidth + 'px', transform: 'translate3d(' + sliderTrans + ', 0, 0)'}">
      <view v-if="useContentSlider"  class="tab-part-bar-slider" :style="{width: sliderPartWidth + 'px'}"></view>
    </view>
  </view>
</template>

<script>
/**
 * Easy Tabbar Component
 * @author Snoop Zhang (github: https://github.com/zy0228)
 * @property {Array} data 
 *  label [string] *required
 *  icon [string]
 *  value [Number] *required
 * @property {Number} value actived value
 * @property {Boolean} showSlider show bottom slider
 * @property {Boolean} useTransition
 * @property {Boolean} useContentSlider make shure showSlider value is true
 */
const COMPONENT_NAME = 'easy-tab-bar'

const EVENT_CLICK = "tabClick"

export default {
  name: COMPONENT_NAME,
  props: {
    data: {
      type: Array,
      default() {
        return []
      }
    },
    value: {
      type: [String, Number],
      default: 0
    },
    inline: {
      type: Boolean,
      default: false
    },
    showSlider: {
      type: Boolean,
      default: true
    },
    useTransition: {
      type: Boolean,
      default: true
    },
    useContentSlider: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      sliderWidth: 0,
      sliderTrans: 0,
      sliderPartWidth: 0
    }
  },
  computed: {
    showSliderCls() {
      return this.useContentSlider ? 'noBackground' : ''
    }
  },
  created() {
    this.tabs = [];
  },
  mounted() {
    setTimeout(() => {
      this._updateSliderStyle()
    }, 20)
  },
  watch: {
    value() {
      this._updateSliderStyle();
    }
  },
  methods: {
    addTab(tab) {
      this.tabs.push(tab)
    },
    setFirstSliderPartWidth(width) {
      this.partSliderWidth = width
    },
    trigger(value, sliderWidth) {
      this.partSliderWidth = sliderWidth
      this.$emit(EVENT_CLICK, value)
    },
    _updateSliderStyle() {
      if (!this.showSlider) return;
      const { width, index } = this._getSliderWidthAndIndex();
      this._getAndSetOffsetLeft(index)
    },
    _getSliderWidthAndIndex() {
      const tabs = uni.createSelectorQuery().in(this)

      let width = 0;
      let index = 0;
	  
      if (this.tabs.length > 0) {
        index = this._findIndex(this.tabs, item => item.value === this.value)
        // get .easy-tab all element
        tabs.selectAll('.easy-tab').boundingClientRect(data => {
          width = data[index].width
          this.sliderWidth = width
          // showPartSlider
          if (this.useContentSlider) {
            this.sliderPartWidth = this.partSliderWidth
          }
        }).exec()
      }
      return {
        width,
        index
      };
    },
    _findIndex(arr, compare) {
      return arr.findIndex(compare)
    },
    _getAndSetOffsetLeft(index) {
      let width
      const tabs = uni.createSelectorQuery().in(this)
      tabs.selectAll('.easy-tab').boundingClientRect(data => {
        // 因为小程序获取不到offesetleft属性 所以要执行left-isPading以0为基点
        const isPadding = data[0].left
        width = data[index].left || 0
        if (this.useTransition)
          this.sliderTrans = isPadding ? `${width - isPadding}px` : `${width}px`
      }).exec()
    },
		setSliderTransform(offsetX) {
			console.log(offsetX)
			this.sliderTrans = offsetX + 'px'
		}
  }
}
</script>

<style lang="scss" scoped>
.easy-tab-bar {
  position: relative;
  display: flex;
  align-items: center;
  height: 100%;
  justify-content: center;
}

.easy-tab-bar_inline {
  border-bottom: #EEEEEE 1rpx solid;
}

.easy-tab {
  display: flex;
  height: 100%;
  align-content: center;
  justify-content: center;
  align-items: center;
}

.easy-tab {
  flex: 1;
  padding: 7px 0;
  text-align: center;
}

.easy-tab-bar-slider {
  position: absolute;
  left: 0;
  bottom: 0;
  height: 2px;
  display: flex;
  justify-content: center;
  width: 20px;
  background-color: red;
  transition: transform 0.2s linear;
  .tab-part-bar-slider{
    height: 2px;
    background-color: red;
    transition: width .2s linear;
  }
}

.noBackground {
  background: none!important;
}
</style>
