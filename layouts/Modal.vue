<template>
  <transition name="modal--fade">
    <div @click.self="close" class="modal__backdrop">
      <article
        :style="{ width }"
        class="modal__container"
        role="dialog"
        aria-labelledby="modalTitle"
        aria-describedby="modalDescription"
      >
        <header class="modal__header">
          <slot name="header" />
          <button @click="close" class="btn-icon">
            <font-awesome-icon :icon="['fas', 'times']" />
          </button>
        </header>
        <div class="modal__content">
          <slot name="content" />
        </div>
        <footer class="modal__footer">
          <slot name="footer" />
        </footer>
      </article>
    </div>
  </transition>
</template>

<script>
export default {
  props: {
    width: {
      type: String,
      required: false,
      default: 'auto',
    },
  },
  methods: {
    close() {
      this.$emit('close')
    },
  },
}
</script>

<style lang="stylus" scoped>
@import '../assets/styles/chore/color.styl'
@import '../assets/styles/chore/elements.styl'

.modal__backdrop
  position fixed
  z-index 9999
  top 0
  bottom 0
  left 0
  right 0
  background-color rgba(#000000, 0.6)
  display flex
  justify-content center
  align-items center

.modal__container
  background-color bg
  border 2px solid primary
  display flex
  flex-direction column
  justify-content space-between
  border-radius radius
  min-width 20rem
  max-width 100vw
  min-height 10rem
  padding 15px

.modal__header
  display flex
  justify-content space-between
  align-items center
  color primary
  font-weight 600
  font-size 1.3rem

.modal__content
  margin-bottom 2rem

.modal--fade-enter, .modal--fade-leave-active
  opacity 0
  top -10px

.modal--fade-enter-active, .modal--fade-leave-active
  transition all .4s ease
</style>
