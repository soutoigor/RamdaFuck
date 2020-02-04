<template>
  <Fragment>
    <div class="accessibility__container">
      <transition name="menuAccessiblity">
        <ul v-show="openMenu" class="accessibility__box">
          <li>
            <button
              :disabled="actualFontSize === 14"
              @click="changeFontSize('decrease')"
              class="btn-icon"
            >
              <font-awesome-icon
                :icon="['fas', 'font']"
                class="accessibility__icon"
              />
              <font-awesome-icon
                :icon="['fas', 'minus']"
                class="accessibility__icon___operator"
              />
            </button>
          </li>
          <li>
            <button
              :disabled="actualFontSize === 20"
              @click="changeFontSize('increase')"
              class="btn-icon"
            >
              <font-awesome-icon
                :icon="['fas', 'font']"
                class="accessibility__icon"
              />
              <font-awesome-icon
                :icon="['fas', 'plus']"
                class="accessibility__icon___operator"
              />
            </button>
          </li>
          <li>
            <button @click="changeFontSize('reset')" class="btn-icon">
              <font-awesome-icon :icon="['fas', 'sync']" />
            </button>
          </li>
          <!-- <li>
            <button @click="changeTheme" for="theme-changer" class="btn-icon">
              <transition name="themeIcon" mode="out-in">
                <font-awesome-icon
                  key="sun"
                  v-if="isDark"
                  :icon="['fas', 'sun']"
                />
                <font-awesome-icon key="moon" v-else :icon="['fas', 'moon']" />
              </transition>
            </button>
          </li> -->
        </ul>
      </transition>
      <div class="accessibility__box">
        <button
          @click="openMenu = !openMenu"
          for="theme-changer"
          class="btn-icon"
        >
          <font-awesome-icon
            :icon="['fas', 'cog']"
            class="accessibility__cog-icon"
          />
        </button>
      </div>
    </div>
  </Fragment>
</template>

<script>
import { Fragment } from 'vue-fragment'
import { cond, not, isNil, add, subtract, always, equals } from 'ramda'

export default {
  components: {
    Fragment,
  },
  data() {
    return {
      isDark: false,
      actualFontSize: null,
      openMenu: false,
    }
  },
  mounted() {
    if (not(isNil(this.getFontSizeLocalStorage()))) {
      this.changeFontSize('load')
    }
  },
  methods: {
    rootElement() {
      return document.querySelector('html')
    },
    getRootFontSize() {
      const style = window
        .getComputedStyle(this.rootElement(), null)
        .getPropertyValue('font-size')
      return parseFloat(style)
    },
    setFontSizeLocalStorage(size) {
      localStorage.setItem('root_font_size', size)
    },
    getFontSizeLocalStorage() {
      return parseFloat(localStorage.getItem('root_font_size'))
    },
    changeFontSize(operation) {
      const root = this.rootElement()
      const fontSize = this.getRootFontSize()
      const changedFontSize = cond([
        [equals('increase'), always(add(1, fontSize))],
        [equals('decrease'), always(subtract(fontSize, 1))],
        [equals('reset'), always(16)],
        [equals('load'), always(this.getFontSizeLocalStorage())],
      ])(operation)
      this.actualFontSize = changedFontSize
      root.style.fontSize = `${changedFontSize}px`
      this.setFontSizeLocalStorage(changedFontSize)
    },
    changeTheme() {
      this.isDark = !this.isDark
    },
  },
}
</script>

<style lang="stylus" scoped>
@import '../assets/styles/chore/color.styl'
@import '../assets/styles/chore/elements.styl'

break-point = 800px

.accessibility__container
  display flex
  flex-direction row-reverse
  opacity 0.6
  transition all .3s linear
  &:hover, &:active
    opacity 1
    transition @transition

.accessibility__box
  display flex
  flex-direction row
  justify-content space-around
  align-items center
  background-color bg
  border-right 1px solid primary
  border-bottom @border-right
  width auto
  height 2rem
  padding .5rem 0

.accessibility__icon
  font-size .9rem

.accessibility__icon___operator
  margin-bottom .6rem

.btn-icon
  width 3rem
  margin 0 .3rem
  height @width
  color font-color
  disabledStyle()


.accessibility__cog-icon
  font-size 1.4rem
  transition all .2s linear
  &:hover
    transform rotateZ(90deg)
    transition @transition

.accessibility__btn-theme
  cursor pointer
  padding .8rem

.themeIcon-enter-active, .themeIcon-leave-active {
  transition all .2s linear
}
.themeIcon-enter, .themeIcon-leave-to {
  opacity 0
  transform translateY(-15px)
}

.menuAccessiblity-enter-active, .menuAccessiblity-leave-active {
  transition all .3s linear
}
.menuAccessiblity-enter, .menuAccessiblity-leave-to {
  opacity 0
  transform translateX(-20rem)
}
</style>
