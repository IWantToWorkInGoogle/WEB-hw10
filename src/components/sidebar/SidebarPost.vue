<template>
  <section>
    <div class="header">
      {{ post.title }}
    </div>
    <div class="body">
      {{ post.text }}
    </div>
    <div class="footer">
      <a href="#" @click.prevent="changeToPost(post)">View all</a>
    </div>
  </section>
</template>

<script>
export default {
  name: "SidebarPost",
  props: ["post"],
  methods: {
      changeToPost: function () {
          this.$root.$emit("returnPost", this.post);

      }
  }
}
</script>

<style scoped>
section {
  margin-bottom: 1rem;
}
</style>