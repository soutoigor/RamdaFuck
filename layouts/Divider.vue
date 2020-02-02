<template>
  <div class="divider__container">
    <div class="divider__line"></div>
    <img src="~assets/logo-ramda.png" class="divider__image" />
    <div class="divider__line"></div>
  </div>
</template>

<style lang="stylus" scoped>
@import '../assets/styles/chore/color.styl'

.divider__container
  display flex
  justify-content center
  align-items center

.divider__image
  width 30px
  margin 0 40px

.divider__line
  width 100%
  height 2px
  background-color primary
</style>
