<template>
  <header class="header__container">
    <img class="header__image" src="~/assets/ramdafuck-black.png" />
    <nav class="header__nav___container">
      <ul>
        <li>
          <nuxt-link class="anchor-link" to="/about">
            About
          </nuxt-link>
        </li>
        <li>
          <a
            class="anchor-link"
            target="_blank"
            href="https://github.com/soutoigor"
          >
            Fork Me
          </a>
        </li>
      </ul>
    </nav>
  </header>
</template>

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
