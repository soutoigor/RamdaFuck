<template>
  <Fragment>
    <button @click="handleModal(true)" class="button__container bold">
      <font-awesome-icon :icon="['fas', 'plus']" class="button__icon" />
      New RamdaFuck
    </button>
    <keep-alive>
      <modal v-show="newPostModal" @close="handleModal(false)" width="30vw">
        <h2 slot="header">New RamdaFuck</h2>
        <div slot="content">
          <div class="fields__container">
            <input
              v-model="title"
              class="input fields"
              type="text"
              placeholder="Post title"
            />
            <textarea
              v-model="description"
              class="input fields textarea"
              rows="2"
              type="text"
              placeholder="Post description (optional)"
            />
            <input
              v-model="authorName"
              class="input fields"
              type="text"
              placeholder="Your name"
            />
            <h3 class="bold fields__code-label">The code:</h3>
            <prism-editor
              v-if="newPostModal"
              v-model="code"
              class="fields__code"
              language="js"
            />
          </div>
          <div slot="footer" class="footer">
            <button
              :disabled="shouldDisableButton"
              @click="newPost"
              class="btn btn-primary"
            >
              Post!
            </button>
          </div>
        </div>
      </modal>
    </keep-alive>
  </Fragment>
</template>

<script>
import { Fragment } from 'vue-fragment'
import PrismEditor from 'vue-prism-editor'
import Modal from '~/layouts/Modal'

export default {
  components: {
    Modal,
    PrismEditor,
    Fragment,
  },
  data() {
    return {
      authorName: '',
      code: '',
      title: '',
      description: '',
      newPostModal: false,
    }
  },
  computed: {
    shouldDisableButton() {
      return !this.authorName || !this.code || !this.title
    },
  },
  methods: {
    handleModal(value) {
      this.newPostModal = value
    },
    async newPost() {
      const newPost = {
        authorName: this.authorName,
        code: this.code,
        title: this.title,
        description: this.description,
        like: 0,
      }
      const post = await this.$axios.$post('/post', newPost)
      this.cleanData()
      this.handleModal(false)
      this.$emit('newPost', post)
    },
    cleanData() {
      this.authorName = ''
      this.code = ''
      this.title = ''
      this.description = ''
      this.newPostModal = ''
    },
  },
}
</script>

<style lang="stylus" scoped>
@import '../assets/styles/chore/color.styl'

transition()
  transition all .2s linear

.button__container
  background-color bg
  border none
  font-size 1.2rem
  color secondary
  display flex
  align-items center
  transition()
  &:hover
    color primary
    .button__icon
      color bg
      background-color primary
      border-radius 4px
      transition()

.fields__container
  display flex
  flex-direction column
  align-items center
  margin-top 2rem
  padding 0 1rem

.fields
  margin .5rem 0
  width 100%

.fields__code
  margin-top .5rem
  padding-bottom 1rem
  width 100%

.button__icon
  color primary
  margin-right 1rem
  font-size 1.5rem
  padding .3rem
  transition()

.footer
  margin-top 1.4rem
  display flex
  justify-content center

.fields__code-label
  margin-top .8rem
  width 100%
  color primary
</style>
