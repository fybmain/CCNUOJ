<template>
  <el-input
    v-html="renderedText"
    class="markdown-text"
    type="textarea"
    :readonly="true"
    autosize
    placeholder="文本为空"
    ref="markdown-area"
  >
  </el-input>
</template>

<script>
import marked from 'marked';

export default {
  name: 'MarkdownViewer',
  props: {
    value: String,
  },
  computed: {
    renderedText() {
      return marked(this.value, { sanitize: true });
    },
  },
  methods: {
    callMathJax() {
      this.$nextTick(() => {
        window.MathJax.Hub.Queue([
          'Typeset',
          window.MathJax.Hub,
          this.$refs['markdown-area'].name,
        ]);
      });
    },
  },
  mounted() {
    this.callMathJax();
  },
  watch: {
    value() {
      this.callMathJax();
    },
  },
};

</script>

<style>
.markdown-text {
  text-align: left;
  font-size: 20px;
}

.MathJax{
  outline:0;
}

</style>
