<template>
  <div style="max-height: 400px">
    <TipTap :content=model.content :update="update"/>
  </div>
</template>

<script>
import TipTap from './TipTap'

export default {
  mixins: [window.Storyblok.plugin],
  components: {
    TipTap
  },
  methods: {
    initWith() {
      return {
        // needs to be equal to your storyblok plugin name
        plugin: 'tiptap-editor',
        content: {}
      }
    },
    update(content) {
      this.model.content = content
    }
  },
   beforeDestroy() {
    this.editor.destroy()
  },
  watch: {
    'model': {
      handler: function (value) {
        this.$emit('changed-model', value);
      },
      deep: true
    }
  }
}
</script>

<style>
</style>
