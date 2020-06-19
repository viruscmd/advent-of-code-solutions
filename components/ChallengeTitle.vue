<template>
  <div>
    <h1 class="subtitle has-text-grey-light">{{subtitle}}</h1>
    <h2 class="title">{{title}}
      <br class="is-hidden-desktop">
      <a class="challenge-link" :href="link">
        <b-icon icon="link-variant" size="is-small"></b-icon>&nbsp;view&nbsp;challenge
      </a>
    </h2>
  </div>
</template>

<script>
  export default {
    name: "challenge-title",
    props: {
        title: String,
        subtitle: String,
        link: String,
    }
  }
</script>

<style scoped>

</style>
