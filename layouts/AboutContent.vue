<template>
  <section class="about">
    <article class="about__article">
      <h1 class="article__title">About RamdaFuck</h1>
      <p class="article__paragraph">
        Me and my friends from work always liked to share "RamdaFucks" between
        us, and we also had created a slack channel only to post them!
      </p>
      <p class="article__paragraph">
        So I thought "Why not creating a page to save it without the risk of
        losing it? And then external people can contribute".
      </p>
      <p class="article__paragraph">And that's it. 🤓</p>
    </article>
    <article class="about__article">
      <h1 class="article__title">What is Ramda</h1>
      <p class="article__paragraph">
        Ramda is an incredible functional library, that helps you with
        functional programming in JavaScript.
      </p>
      <p class="article__paragraph">
        You can see its documentation
        <a href="https://ramdajs.com/" target="_blank">here</a>.
      </p>
    </article>
    <article class="about__article">
      <h1 class="article__title">Why RamdaFuck?</h1>
      <p class="article__paragraph">
        We say "RamdaFuck" for when a function made with Ramda gets so big,
        nested and confuse, that it gets unreadable and worst that if not using
        Ramda.
      </p>
      <p class="article__paragraph">Just like the "callback hell" 👹</p>
    </article>
  </section>
</template>

<style lang="stylus" scoped>
.about
  display flex
  flex-direction column
  align-items center
  padding-top 1rem

.about__article
  margin-top 2rem
  width 45vw
  @media screen and (max-width: 930px)
    width 90vw

.article__title
  font-size 2rem
  font-weight 600
  margin-bottom .7rem

.article__paragraph
  line-height 1.8rem
  font-size 1.1rem
</style>
