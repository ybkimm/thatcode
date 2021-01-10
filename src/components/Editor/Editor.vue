<template>
  <div class="editor">
    <pre
      class="editor-view"
      :style="{ top: `${-scrollPos[0]}px`, left: `${-scrollPos[1]}px` }"
    ><code v-html="rendered"/></pre>
    <textarea
      class="editor-code"
      autocomplete="off"
      autocorrect="off"
      autocapitalize="off"
      spellcheck="false"
      ref="srcElement"
      v-model="src"
      @click="selectionchange"
      @scroll="onScroll"
    />
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, ref } from 'vue'

import Prism from 'prismjs'

export default defineComponent({
  setup() {
    const srcElement = ref<HTMLTextAreaElement | null>(null)
    const src = ref(
      'p { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; } p { margin: 0; } p { margin: 0; } p { margin: 0; } p { margin: 0; } p { margin: 0; } p { margin: 0; } p { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }\np { margin: 0; }'
    )
    const scrollPos = ref<[number, number]>([0, 0])

    const rendered = computed(() =>
      Prism.highlight(src.value, Prism.languages.css, 'css')
    )

    const onScroll = () => {
      const src = srcElement.value
      if (src == null) {
        return
      }
      scrollPos.value = [src.scrollTop, src.scrollLeft]
    }

    const selectionchange = () => {
      const el = srcElement.value
      if (el == null) {
        return
      }
      console.log(`${el.selectionStart} / ${el.selectionEnd}`)
    }

    return {
      srcElement,
      src,
      rendered,
      selectionchange,
      scrollPos,
      onScroll
    }
  }
})
</script>

<style lang="scss" scoped>
$background-color: #1d1f21;
$code-color: #ffffff;
$selection-color: #ffffff;
$selection-background: #ff9800;

.editor {
  position: relative;
  width: 100%;
  height: 100%;
  box-sizing: border-box;
  color: $code-color;
  background-color: $background-color;
  overflow: hidden;

  .editor-view,
  .editor-code {
    position: absolute;
    top: 0;
    left: 0;
  }

  .editor-view,
  .editor-code,
  .editor-view code {
    font-family: D2Coding, monospace;
  }

  .editor-view {
    margin: 0;
  }

  .editor-code {
    width: 100%;
    height: 100%;
    border: 0;
    padding: 0;
    background: transparent;
    color: transparent;
    caret-color: $code-color;
    resize: none;
    box-sizing: border-box;
    white-space: nowrap;

    &::selection {
      color: $selection-color;
      background-color: $selection-background;
    }

    &:focus {
      outline: none;
    }
  }
}
</style>

<style>
/**
 * atom-dark theme for `prism.js`
 * Based on Atom's `atom-dark` theme: https://github.com/atom/atom-dark-syntax
 * @author Joe Gibson (@gibsjose)
 */

code[class*='language-'],
pre[class*='language-'] {
  color: #c5c8c6;
  text-shadow: 0 1px rgba(0, 0, 0, 0.3);
  font-family: inherit;
  direction: ltr;
  text-align: left;
  white-space: pre;
  word-spacing: normal;
  word-break: normal;
  line-height: 1.5;

  -moz-tab-size: 4;
  -o-tab-size: 4;
  tab-size: 4;

  -webkit-hyphens: none;
  -moz-hyphens: none;
  -ms-hyphens: none;
  hyphens: none;
}

/* Code blocks */
pre[class*='language-'] {
  padding: 1em;
  margin: 0.5em 0;
  overflow: auto;
  border-radius: 0.3em;
}

:not(pre) > code[class*='language-'],
pre[class*='language-'] {
  background: #1d1f21;
}

/* Inline code */
:not(pre) > code[class*='language-'] {
  padding: 0.1em;
  border-radius: 0.3em;
}

.token.comment,
.token.prolog,
.token.doctype,
.token.cdata {
  color: #7c7c7c;
}

.token.punctuation {
  color: #c5c8c6;
}

.namespace {
  opacity: 0.7;
}

.token.property,
.token.keyword,
.token.tag {
  color: #96cbfe;
}

.token.class-name {
  color: #ffffb6;
  text-decoration: underline;
}

.token.boolean,
.token.constant {
  color: #99cc99;
}

.token.symbol,
.token.deleted {
  color: #f92672;
}

.token.number {
  color: #ff73fd;
}

.token.selector,
.token.attr-name,
.token.string,
.token.char,
.token.builtin,
.token.inserted {
  color: #a8ff60;
}

.token.variable {
  color: #c6c5fe;
}

.token.operator {
  color: #ededed;
}

.token.entity {
  color: #ffffb6;
  cursor: help;
}

.token.url {
  color: #96cbfe;
}

.language-css .token.string,
.style .token.string {
  color: #87c38a;
}

.token.atrule,
.token.attr-value {
  color: #f9ee98;
}

.token.function {
  color: #dad085;
}

.token.regex {
  color: #e9c062;
}

.token.important {
  color: #fd971f;
}

.token.important,
.token.bold {
  font-weight: bold;
}

.token.italic {
  font-style: italic;
}
</style>
