<template>
    <div class="middle">
        <Sidebar :posts="viewPosts"/>
        <main>
            <Index v-if="page === 'Index'" :currentPost="null"
                   :posts="viewAllPosts" :comments="viewComments"/>
            <Enter v-if="page === 'Enter'"/>
            <Registration v-if="page === 'Registration'"/>
            <WritePost v-if="page === 'WritePost'"/>
            <EditPost v-if="page === 'EditPost'"/>
            <Users v-if="page === 'Users'" :users="viewUsers"/>
            <Post v-if="page === 'Post'" :currenPost="this.currentPost" :post="this.currentPost"
                        :comments="commentsOfPost(this.currentPost.id)"
                        :userId="this.userId"/>
        </main>
    </div>
</template>

<script>
import Sidebar from "./sidebar/Sidebar";
import Index from "./page/Index";
import Enter from "./page/Enter";
import WritePost from "./page/WritePost";
import EditPost from "./page/EditPost";
import Registration from "./page/Registration";
import Users from "./users/Users.vue";
import Post from "@/components/post/Post.vue";

export default {
    name: "Middle",
    data: function () {
        return {
            page: "Index"
        }
    },
    components: {
      Post,
        Users,
        Registration,
        WritePost,
        Enter,
        Index,
        Sidebar,
        EditPost
    },
    props: ["posts","users","comments","currentPost","userId"],
    computed: {
        viewPosts: function () {
            return Object.values(this.posts).sort((a, b) => b.id - a.id).slice(0, 2);
        },
        viewAllPosts: function () {
            return Object.values(this.posts).sort((a,b) => b.id - a.id);
        },
        viewUsers: function () {
            return Object.values(this.users);
        },
        viewComments: function () {
            return Object.values(this.comments);
        }
    },
    methods: {
        commentsOfPost(postId) {
            return Object.values(this.comments).filter(u => u.currentPost.id === postId);
        }
    },
    beforeCreate() {
        this.$root.$on("onChangePage", (page) => {
            this.page = page;
            alert(page);
            this.$forceUpdate();
        });
    }
}
</script>

<style scoped>

</style>
