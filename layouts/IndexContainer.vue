<template>
  <main>
    <section class="index__main">
      <div class="index__new-ramdafuck">
        <new-ramdafuck @newPost="setNewPost" />
      </div>
      <div class="index__post-list">
        <post-container :new-post="newPost" />
      </div>
    </section>
    <aside>
      <accessibility-area />
    </aside>
  </main>
</template>

<script>
import NewRamdafuck from '~/components/NewRamdafuck'
import PostContainer from '~/components/PostContainer'
import AccessibilityArea from '~/layouts/AccessibilityArea'

export default {
  components: {
    NewRamdafuck,
    PostContainer,
    AccessibilityArea,
  },
  data() {
    return {
      newPost: {},
    }
  },
  methods: {
    setNewPost(post) {
      this.newPost = post
    },
  },
}
</script>

<style lang="stylus" scoped>

.index__main
  display flex
  flex-direction column
  align-items center

.index__new-ramdafuck
  display flex
  justify-content center
  margin 3rem 0
  @media screen and (max-width: 930px){
    margin 3rem 0 1.5rem 0
  }

.index__post-list
  margin-bottom 4rem
  width auto
</style>
