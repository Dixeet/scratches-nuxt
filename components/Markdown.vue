<template>
  <div class="markdown" v-html="html" />
</template>

<script>
import marked from 'marked';
import hljs from 'highlight.js';
import 'highlight.js/styles/railscasts.css';

marked.setOptions({
  gfm: true,
  breaks: true,
  highlight(code, lang) {
    if (lang) {
      return hljs.highlight(lang, code).value
    }
    return hljs.highlightAuto(code).value;
  },
});

export default {
  props: {
    md: {
      type: String,
      required: true,
    },
  },
  computed: {
    html() {
      return marked(this.md);
    },
  },
};
</script>

<style lang="scss">
.markdown {
  p, pre, h1, h2, h3 {
    margin-bottom: 1.25rem;
  }
  h1 {
    font-size: 2rem;
  }
  h2 {
    font-size: 1.5rem;
  }
  h3 {
    font-size: 1.25rem;
  }
}
</style>
