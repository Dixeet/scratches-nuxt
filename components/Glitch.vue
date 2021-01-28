<template>
  <div class="glitch" :data-text="text" :style="style">
    <slot></slot>
  </div>
</template>

<script>
import _get from 'lodash/get';

export default {
  props: {
    background: {
      type: String,
      default: '',
    },
    textShadowBefore: {
      type: String,
      default: '',
    },
    textShadowAfter: {
      type: String,
      default: '',
    },
    textShadowWidth: {
      type: String,
      default: '',
    },
  },
  data() {
    const text = _get(this.$slots, 'default[0].text', '');
    return {
      text,
    };
  },
  computed: {
    style() {
      return (
        // eslint-disable-next-line prefer-template
        '' +
        (this.background ? `--text-background: ${this.background};` : '') +
        (this.textShadowAfter ? `--text-shadow-after: ${this.textShadowAfter};` : '') +
        (this.textShadowBefore ? `--text-shadow-before: ${this.textShadowBefore};` : '') +
        (this.textShadowWidth ? `--text-shadow-width: ${this.textShadowWidth};` : '')
      );
    },
  },
};
</script>

<style lang="scss" scoped>
.glitch {
  position: relative;
  --text-shadow-after: red;
  --text-shadow-before: blue;
  --text-background: black;
  --text-shadow-width: 1px;
  white-space: nowrap;
  display: inline-block;

  &:after {
    content: attr(data-text);
    position: absolute;
    left: 2px;
    text-shadow: calc(var(--text-shadow-width) * -1) 0 var(--text-shadow-after);
    top: 0;
    background: var(--text-background);
    overflow: hidden;
    clip: rect(0, 900px, 0, 0);
    animation: noise-anim 2s infinite linear alternate-reverse;
  }
  &:before {
    content: attr(data-text);
    position: absolute;
    left: -2px;
    text-shadow: var(--text-shadow-width) 0 var(--text-shadow-before);
    top: 0;
    background: var(--text-background);
    overflow: hidden;
    clip: rect(0, 900px, 0, 0);
    animation: noise-anim-2 3s infinite linear alternate-reverse;
  }
}
@keyframes noise-anim {
  $steps: 20;
  @for $i from 0 through $steps {
    #{percentage($i*(1/$steps))} {
      clip: rect(random(100) + px, 9999px, random(100) + px, 0);
    }
  }
}

@keyframes noise-anim-2 {
  $steps: 20;
  @for $i from 0 through $steps {
    #{percentage($i*(1/$steps))} {
      clip: rect(random(100) + px, 9999px, random(100) + px, 0);
    }
  }
}
</style>
