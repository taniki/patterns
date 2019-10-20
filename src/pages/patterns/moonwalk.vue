<template>
  <LayoutPattern
    :title="title"
    :component="pattern"
  />
</template>

<script>
import LayoutPattern from '~/layouts/pattern'
import PatternMoonwalk from '~/patterns/moonwalk'

export default {
  components: { LayoutPattern },
  data () {
    return {
      title: 'Moonwalk',
      pattern: PatternMoonwalk
    }
  }
}
</script>
