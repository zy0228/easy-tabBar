<template>
  <view class="easy-tab" @click="handleClick" :class="{'easy-tab_active': isActive}">
    <slot>
      <i :class="icon"></i>
    </slot>
    <slot>
      <view v-html="label" class="slider-content"></view>
    </slot>
  </view>
</template>

<script>
const COMPONENT_NAME = 'easy-tab'

export default {
  name: COMPONENT_NAME,
  props: {
    label: {
      type: [String, Number],
      require: true
    },
    value: {
      type: [String, Number],
      require: true
    },
    icon: {
      type: String,
      default: ''
    },
    showCntSlider: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      firstSlideWidth: 0
    }
  },
  computed: {
    isActive () {
      return this.$parent.value === this.value
    }
  },
  mounted() {
    this.$parent.addTab(this)
    //init slider width
    if (this.isActive && this.showCntSlider) {
      const tabContent = uni.createSelectorQuery().in(this)
      tabContent.select('.slider-content').boundingClientRect(data => {
        this.$parent.setFirstSliderPartWidth(data.width)
      }).exec()
    }
  },
  methods: {
    handleClick() {
      const sliderContent = uni.createSelectorQuery().in(this)
      sliderContent.select('.slider-content').boundingClientRect(data => {
        this.$parent.trigger(this.value, data.width || 0)
      }).exec()
    }
  }
}
</script>

<style lang="scss" scoped>
.easy-tab {
  position: relative;
  // flex: 1;
  padding: 7px 0;
  color: #666; /**use theme color */
  text-align: center;
  font-size: 18;
  font-weight: 500;
}

.easy-tab::before {
  content: '';
  position: absolute;
  top: -20rpx;
  left: -20rpx;
  right: -20rpx;
  bottom: -20rpx;
}

.easy-tab_active {
  font-weight: bold;
  color: red!important; /**use thene color */
}
</style>