<template>
  <div class="thatcode">
    <div class="editor-wrapper">
      <Editor />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

import Editor from './components/Editor'

export default defineComponent({
  components: {
    Editor
  }
})
</script>

<style>
html,
body,
#app {
  height: 100%;
  width: 100%;
  margin: 0;
  padding: 0;
  overflow: hidden;
  font-size: 16px;
  user-select: none;
}
</style>

<style lang="scss" scoped>
.thatcode {
  display: grid;
  width: 100%;
  height: 100%;
  grid-template-columns: minmax(0, 1fr);
  grid-template-rows: minmax(0, 1fr) 10rem;

  .editor-wrapper {
    grid-column: 1 / 2;
    grid-row: 1 / 2;
  }
}
</style>
