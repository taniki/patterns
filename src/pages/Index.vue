<template>
  <Layout>
    <g-link to="/patterns/moonwalk">
      <component
        is="PatternMoonwalk"
        class="fl w-third"
      />
    </g-link>
  </Layout>
</template>

<script>

import PatternMoonwalk from '~/patterns/moonwalk'

export default {
  components: { PatternMoonwalk },
  metaInfo: {
    title: 'Hello, world!'
  }
}
</script>

<style>
.home-links a {
  margin-right: 1rem;
}
</style>
