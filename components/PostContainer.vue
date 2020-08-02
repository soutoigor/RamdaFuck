<template>
  <section>
    <h2 v-if="feedIsEmpty" class="bold subtitle">
      There's no posts yet :(
    </h2>
    <img v-if="isLoading" src="~assets/spinner.svg" alt="load" />
    <transition-group name="newPost" tag="div">
      <div v-for="item of list" :key="item._id">
        <post-template
          :post="item"
          @newComment="newComment"
          class="post__template"
        />
        <div class="post__comment-title">
          <span v-if="hasComments(item.comments)" class="bold underline">
            Comments
          </span>
        </div>
        <transition-group name="newComment">
          <div v-for="comment of item.comments" :key="comment.message">
            <comments-list :comment="comment" class="post__comment" />
          </div>
        </transition-group>
        <divider v-if="shouldShowDivider(item)" />
      </div>
    </transition-group>
  </section>
</template>

<script>
import { map, propEq, reverse, and, isEmpty, not, equals, last } from 'ramda'
import PostTemplate from '~/layouts/PostTemplate'
import CommentsList from '~/layouts/CommentsList'
import Divider from '~/layouts/Divider'

export default {
  components: {
    PostTemplate,
    CommentsList,
    Divider,
  },
  props: {
    newPost: {
      type: Object,
      required: false,
      default: null,
    },
  },
  data() {
    return {
      list: [],
      isLoading: false,
    }
  },
  computed: {
    feedIsEmpty() {
      return and(isEmpty(this.list), not(this.isLoading))
    },
  },
  watch: {
    newPost(data) {
      this.list.unshift(data)
    },
  },
  created() {
    this.getPostList()
  },
  methods: {
    hasComments(comments) {
      return not(isEmpty(comments))
    },
    shouldShowDivider(item) {
      return not(equals(item, last(this.list)))
    },
    newComment({ comment, id }) {
      this.list = map((item) => {
        if (propEq('_id', id, item)) {
          item.comments.push(comment)
        }
        return item
      }, this.list)
    },
    async getPostList() {
      this.isLoading = true
      const actualList = await this.$axios.$get('/post')
      this.list = reverse(actualList)
      this.isLoading = false
    },
  },
}
</script>

<style lang="stylus" scoped>
.post__template
  margin 3rem 0

.post__comment-title
  display flex
  justify-content center

.post__comment
  margin 2.2rem 0

.newPost-enter-active, .newPost-leave-active {
  transition all 1s
}
.newPost-enter, .newPost-leave-to {
  opacity 0
  transform translateY(-70px)
}

.newComment-enter-active, .newComment-leave-active {
  transition all 1s
}
.newComment-enter, .newComment-leave-to {
  opacity 0
  transform translateX(-70px)
}
</style>
