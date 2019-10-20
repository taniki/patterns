<template>
  <layout>
    <slot>
      <component
        :is="pattern"
        v-model="parameters"
        @parameters="setParameters"
      />

      <PatternControls v-model="parameters" />

      <div class="mw9 center pa3 pa3-ns">
        <h2 class="avenir f2 ttu tracked">
          {{ title }}
        </h2>

        <div
          class="measure garamond"
          v-html="parse(doc)"
        />

        <h3 class="avenir f3 ttu tracked">
          Source code
        </h3>
        <div class="code">
          <vue-code-highlight>{{ sourceCode }}</vue-code-highlight>
        </div>
      </div>
    </slot>
  </layout>
</template>

<script>
import Layout from './Default'

import LayoutPattern from '~/layouts/pattern'
import PatternControls from '~/components/PatternControls'
import { component as VueCodeHighlight } from 'vue-code-highlight'

import 'vue-code-highlight/themes/window.css'
import 'vue-code-highlight/themes/prism-tomorrow.css'

import unified from 'unified'
import markdown from 'remark-parse'
import html from 'remark-html'
import breaks from 'remark-breaks'

const $processor = unified()
  .use(markdown)
  .use(breaks)
  .use(html)

export default {
  components: { Layout, LayoutPattern, PatternControls, VueCodeHighlight },
  props: {
    title: String,
    component: Object
  },
  data () {
    return {
      pattern: this.component,
      parameters: {}
    }
  },
  computed: {
    sourceCode () {
      return this.component.methods.draw.toString()
    },
    doc () {
      return this.component.__doc
    }
  },
  mounted () {
  },
  methods: {
    setParameters (e) {
      this.parameters = e
    },
    parse (md) {
      return $processor.processSync(md).toString()
    }
  }
}
</script>
