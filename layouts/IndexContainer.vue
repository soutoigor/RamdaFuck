<template>
  <Fragment>
    <Header class="index__header" />
    <main>
      <section class="index__main">
        <div class="index__new-ramdafuck">
          <new-ramdafuck @newPost="setNewPost" />
        </div>
        <div class="index__post-list">
          <post-container :new-post="newPost" />
        </div>
      </section>
      <aside class="index__accessibility">
        <accessibility-area />
      </aside>
    </main>
  </Fragment>
</template>

<script>
import { Fragment } from 'vue-fragment'
import Header from '~/layouts/Header'
import NewRamdafuck from '~/components/NewRamdafuck'
import PostContainer from '~/components/PostContainer'
import AccessibilityArea from '~/layouts/AccessibilityArea'

export default {
  components: {
    Header,
    NewRamdafuck,
    PostContainer,
    AccessibilityArea,
    Fragment,
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

.index__accessibility
  position fixed
  left 0
  top 25%
</style>
