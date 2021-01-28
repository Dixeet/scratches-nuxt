<template>
  <div class="typing-wrapper">
    <div>
      {{ text }}<noscript>{{ slotText }}</noscript>
      <span :class="{ caret: slotText.length !== text.length || keepCaret }"></span>
    </div>
  </div>
</template>

<script>
import _get from 'lodash/get';

export default {
  props: {
    speed: {
      type: Number,
      default: 50,
    },
    keepCaret: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    const slotText = _get(this.$slots, 'default[0].text', '');
    return {
      slotText,
      text: '',
    };
  },
  mounted() {
    // eslint-disable-next-line prefer-const
    let typeInterval;
    const typing = () => {
      if (this.slotText.length === this.text.length) {
        clearInterval(typeInterval);
      }
      this.text = this.slotText.substring(0, this.text.length + 1);
    };
    typeInterval = setInterval(typing, this.speed);
  },
};
</script>

<style lang="scss" scoped>
.typing-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;

  .caret {
    animation: blink 0.5s step-end infinite alternate;
    border-right: 3px solid;
  }
}
@keyframes blink {
  50% {
    border-color: transparent;
  }
}
</style>
