<template>
  <LayoutPattern
    :title="title"
    :component="pattern"
    :source-code="sourceCode"
  />
</template>

<script>
import LayoutPattern from '~/layouts/pattern'

import PatternMoonwalk from '~/patterns/moonwalk'
import PatternMoonwalkRaw from '!!raw-loader!~/patterns/moonwalk'

export default {
  components: { LayoutPattern },
  data () {
    return {
      title: 'Moonwalk',
      pattern: PatternMoonwalk,
      sourceCode: PatternMoonwalkRaw
    }
  }
}
</script>
