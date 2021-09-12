<template>
  <div class="container-wrap">
    <div class="container">
      <div class="container-title">{{title}}</div>
        <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "container",
  props: {
    title: ""
  }
}
</script>

<style lang="sass" scoped>
.container-wrap
  display: flex
  justify-content: center
  align-items: center
  min-width: 30%
  margin: 0 auto
  .container
    position: relative
    min-width: 10%
    display: inline-block
    border-radius: 25px
    padding: 35px 35px 50px
    background: rgba(255, 255, 255, 0.85)
    z-index: 2
    .container-title
      position: absolute
      top: 0
      left: 35px
      padding: 15px 25px
      border-radius: 15px 15px 0 0
      z-index: 1
      transform: translateY(-100%)
      background: rgba(255, 255, 255, 0.57)
      transition: .3s
    &:hover
      .container-title
        transform: translateY(-95%)
</style>