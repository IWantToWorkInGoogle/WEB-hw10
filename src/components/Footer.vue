<template>
    <footer>
        <p> The number of users : {{ numOfUsers }}</p>
        <p> The number of posts : {{ numOfPosts }}</p>
        <a href="/">Codeforces</a> &copy; 2022 by Mike Mirzayanov
    </footer>
</template>

<script>
export default {
    name: "Footer",
    props: ["numOfUsers","numOfPosts","userId"],

}
</script>

<style scoped>

</style>