<template>
  <div>
      <p>{{comment.userId}}</p>
      <p>{{comment.text}}</p>
  </div>
</template>

<script>
export default {
  name: "Comment",
  props: ["comment"]
}
</script>

<style scoped>

</style>