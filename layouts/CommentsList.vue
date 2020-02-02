<template>
  <div>
    <article class="card comment__container">
      <h3 class="bold">{{ comment.authorName }}</h3>
      <p class="comment__message">{{ comment.message }}</p>
    </article>
  </div>
</template>

<script>
export default {
  props: {
    comment: {
      type: Object,
      required: true,
    },
  },
}
</script>

<style lang="stylus" scoped>
@import '../assets/styles/chore/color.styl'

.comment__container
  border 1px solid lighten(secondary, 50%)
.comment__message
  margin .8rem 0
  line-height 1.5
</style>
