<template>
  <header class="header__container">
    <nuxt-link to="/">
      <img class="header__image" src="~/assets/ramdafuck-black.png" />
    </nuxt-link>
    <nav class="header__nav___container">
      <ul>
        <li v-if="shouldShowLinkBy('/')">
          <nuxt-link class="anchor-link" to="/">
            Home
          </nuxt-link>
        </li>
        <li v-if="shouldShowLinkBy('/about')">
          <nuxt-link class="anchor-link" to="/about">
            About
          </nuxt-link>
        </li>
        <li>
          <a
            class="anchor-link"
            target="_blank"
            href="https://github.com/soutoigor/app.ramdafuck"
          >
            Fork Me
          </a>
        </li>
      </ul>
    </nav>
  </header>
</template>

<script>
export default {
  methods: {
    shouldShowLinkBy(route) {
      return this.$nuxt.$route.path !== route
    },
  },
}
</script>

<style lang="stylus" scoped>
@import '../assets/styles/chore/color.styl'

.header__container
  display flex
  justify-content space-around
  align-items flex-end
  padding .7rem 0
  border-bottom 1px solid secondary

.header__image
  width 170px

.header__nav___container
  margin-bottom 0.625rem
  width 11rem
  font-size 1.4rem
  & ul
    display flex
    justify-content space-between
</style>
