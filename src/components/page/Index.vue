<template>
    <div>
        <Post v-for="post in posts" :currentPost=null :post="post" :key="post.id" :comments="comments"/>
    </div>
</template>

<script>
import Post from "../post/Post";

export default {
    name: "Index",
    components: {
        Post
    },
    props: ["posts", "comments"]
}
</script>

<style scoped>

</style>
