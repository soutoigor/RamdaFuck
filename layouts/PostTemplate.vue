<template>
  <article class="card post__container">
    <header>
      <h2 class="title">{{ postTitle }}</h2>
      <h3 class="subtitle post__subtitle">{{ post.description }}</h3>
    </header>
    <code>
      <prism class="post__code-container" language="js">{{ post.code }}</prism>
    </code>
    <footer class="post__footer">
      <div class="post__actions">
        <div class="post__actions___like-container">
          <font-awesome-icon
            @click="likePost"
            :icon="['fas', 'hand-spock']"
            class="post__actions___like-btn"
          />
          <span class="bold">{{ likes }}</span>
        </div>
        <new-comment @newComment="newComment" />
      </div>
      <span class="bold post__actions___author">{{ post.authorName }}</span>
    </footer>
  </article>
</template>

<script>
import 'prismjs'
import 'prismjs/themes/prism-tomorrow.css'
import Prism from 'vue-prism-component'
import NewComment from '~/components/NewComment'

export default {
  components: {
    Prism,
    NewComment,
  },
  props: {
    post: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      likes: 0,
    }
  },
  computed: {
    postTitle() {
      const { title } = this.post
      return title[0].toUpperCase() + title.slice(1)
    },
  },
  created() {
    this.likes = this.post.like
  },
  methods: {
    async newComment(comment) {
      const parsePost = {
        comments: [
          ...this.post.comments,
          { authorName: comment.authorName, message: comment.message },
        ],
      }
      await this.updatePost(this.post._id, parsePost)
      this.$emit('newComment', { id: this.post._id, comment })
    },
    async likePost() {
      this.likes += 1
      await this.updatePost(this.post._id, { like: this.likes })
    },
    updatePost(postId, property) {
      return this.$axios.$patch(`/post/${postId}`, property)
    },
  },
}
</script>

<style lang="stylus" scoped>
@import '../assets/styles/chore/color.styl'

.post__container
  min-height 12rem

.post__code-container
  border-radius 5px
  min-height 3rem
  display flex
  align-items center

.post__subtitle
  margin 1.3rem 0 .5rem 0

.post__footer
  display flex
  justify-content space-between
  align-items center
  margin-top 1rem

.post__actions
  display flex
  align-items center
  min-width 10rem
  justify-content space-between

.post__actions___like-container
  display flex
  min-width 3rem
  justify-content space-between
  align-items center

.post__actions___like-btn
  color primary
  cursor pointer
  font-size 1.5rem
  &:active
    transform scale(1.2)

.post__actions___author
  width 30%
  text-align right
  white-space wrap
</style>
