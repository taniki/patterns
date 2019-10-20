<template>
  <div>
    <svg
      id="chart"
    />
  </div>
</template>

<script>
import * as d3 from 'd3'

export default {
  props: {
    interactiveParameters: {}
  },
  data () {
    return {
      width: 500,
      height: 500,
      parameters: {
        width: 75,
        size: 3,
        color: '#ddd',
        offset: 15
      }
    }
  },
  computed: {},
  watch: {
    parameters () {
      console.log(this.interactiveParameters)
      console.log('yo')
      this.draw()
    }
  },
  mounted () {
    this.$emit('parameters', this.parameters)

    const chart = d3.select('#chart')
    this.width = chart.node().getBoundingClientRect().width
    this.height = chart.node().getBoundingClientRect().height

    this.draw()
  },
  methods: {
    draw () {
      const chart = d3.select('#chart')

      const gridPoints = []

      for (const x in Array(Math.ceil(this.width / this.parameters.width)).fill()) {
        for (const y in Array(Math.ceil(this.height / this.parameters.width)).fill()) {
          gridPoints.push({
            x: x * this.parameters.width + this.parameters.offset,
            y: y * this.parameters.width + this.parameters.offset
          })

          gridPoints.push({
            x: x * this.parameters.width + 0.5 * this.parameters.width + this.parameters.offset,
            y: y * this.parameters.width + 0.5 * this.parameters.width + this.parameters.offset
          })
        }
      }

      const points = chart.selectAll('circle')
        .data(gridPoints)
        .enter()
        .append('circle')

      points
        .attr('cx', function (d) { return d.x })
        .attr('cy', function (d) { return d.y })
        .attr('r', this.parameters.size)
        .style('fill', this.parameters.color)

      const gridLines = []

      for (const x in Array(Math.ceil(this.width / this.parameters.width)).fill()) {
        gridLines.push({
          x1: x * this.parameters.width + this.parameters.offset,
          y1: 0,
          x2: x * this.parameters.width + this.parameters.offset,
          y2: this.height
        })
      }

      for (const y in Array(Math.ceil(this.height / this.parameters.width)).fill()) {
        gridLines.push({
          x1: 0,
          y1: y * this.parameters.width + this.parameters.offset,
          x2: this.width,
          y2: y * this.parameters.width + this.parameters.offset
        })
      }

      const lines = chart.selectAll('line')
        .data(gridLines)
        .enter()
        .append('line')

      lines
        .attr('x1', d => d.x1)
        .attr('x2', d => d.x2)
        .attr('y1', d => d.y1)
        .attr('y2', d => d.y2)
        .attr('stroke', this.parameters.color)
    }
  }
}
</script>

<style>
svg {
  width: 100%;
  height: 500px;
}
</style>

<doc>
Inspiration: https://www.instagram.com/p/B3x1sysADYN/
</doc>
