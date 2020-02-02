<template>
  <div>
    <span @click="handleCommentModal(true)" class="bold anchor-link">
      Comment
    </span>
    <modal
      v-show="commentModal"
      @close="handleCommentModal(false)"
      width="30vw"
    >
      <h2 slot="header">New comment</h2>
      <div slot="content" class="modal__content">
        <input
          v-model="name"
          class="input fields"
          type="text"
          placeholder="Comment author"
        />
        <textarea
          v-model="comment"
          class="input fields textarea"
          rows="2"
          type="text"
          placeholder="Comment Message"
        />
      </div>
      <div slot="footer" class="modal__footer">
        <button
          :disabled="shouldDisableButtons"
          @click="newComment"
          class="btn btn-primary"
        >
          Post!
        </button>
      </div>
    </modal>
  </div>
</template>

<script>
import Modal from '~/layouts/Modal'

export default {
  components: {
    Modal,
  },
  data() {
    return {
      commentModal: false,
      name: null,
      comment: null,
    }
  },
  computed: {
    shouldDisableButtons() {
      return !this.name || !this.comment
    },
  },
  methods: {
    newComment() {
      const newComment = {
        authorName: this.name,
        message: this.comment,
      }

      this.name = null
      this.comment = null
      this.$emit('newComment', newComment)
      this.handleCommentModal(false)
    },
    handleCommentModal(value) {
      this.commentModal = value
    },
  },
}
</script>

<style lang="stylus" scoped>

.modal__content
  display flex
  flex-direction column
  height 7rem
  margin-top 2rem
  justify-content space-between

.modal__footer
  margin-top 1.4rem
  display flex
  justify-content center
</style>
