<script src="data.js"></script>
<template>
    <div id="app">
        <Header :userId="userId" :users="users"/>
        <Middle :posts="$data.posts" :users="users" :comments="comments" :currentPost="currentPost" :userid="userId"/>
        <Footer :numOfUsers="putNumOfUsers()" :numOfPosts="putNumOfPosts()"/>
    </div>
</template>

<script>
import Header from "./components/Header";
import Middle from "./components/Middle";
import Footer from "./components/Footer";

export default {
    name: 'App',
    components: {
        Footer,
        Middle,
        Header
    },
    data: function () {
        return this.$root.$data;
    },
    methods: {
        putNumOfUsers() {
            return Object.keys(this.users).length;
        },
        putNumOfPosts() {
            return Object.keys(this.posts).length;
        },
    },
    beforeCreate() {
        this.$root.$on("returnPost", (post) => {
            alert(post.id);
            this.currentPost = post;
            this.$root.$emit("onChangePage", "Post");
        });


      this.$root.$on("onEnter", (login, password) => {
            if (password === "") {
                this.$root.$emit("onEnterValidationError", "Password is required");
                return;
            }

            const users = Object.values(this.users).filter(u => u.login === login);
            if (users.length === 0) {
                this.$root.$emit("onEnterValidationError", "No such user");
            } else {
                this.userId = users[0].id;
                this.$root.$emit("onChangePage", "Index");
            }
        });

        this.$root.$on("onRegistration", (login, name) => {

            if (!login || login.length < 3) {
                this.$root.$emit("onRegistrationValidationError", "Login is too short");
                return;
            }

            if (login.length > 16) {
                this.$root.$emit("onRegistrationValidationError", "Login is too long");
                return;
            }

            if (!(/^[a-z]+$/.test(login))) {
                this.$root.$emit("onRegistrationValidationError", "Login must contain only lowercase latin alphabet");
                return;
            }

            if (!name) {
                this.$root.$emit("onRegistrationValidationError", "Name is too short");
                return;
            }

            if (name.length > 32) {
                this.$root.$emit("onRegistrationValidationError", "Name is too long");
                return;
            }

            const users = Object.values(this.users).filter(u => u.login === login);
            if (users.length === 0) {
                const id = Math.max(...Object.keys(this.users)) + 1;
                this.$root.$set(this.users, id, {
                  id, login, name, admin : false
                });
            } else {
                this.$root.$emit("onRegistrationValidationError", "Such user already exists. Change the login");
            }
        });

        this.$root.$on("onLogout", () => this.userId = null);

        this.$root.$on("onWritePost", (title, text) => {
            if (this.userId) {
                if (!title || title.length < 5) {
                    this.$root.$emit("onWritePostValidationError", "Title is too short");
                } else if (!text || text.length < 10) {
                    this.$root.$emit("onWritePostValidationError", "Text is too short");
                } else {
                    const id = Math.max(...Object.keys(this.posts)) + 1;
                    this.$root.$set(this.posts, id, {
                        id, title, text, userId: this.userId
                    });
                }
            } else {
                this.$root.$emit("onWritePostValidationError", "No access");
            }
        });

        this.$root.$on("onEditPost", (id, text) => {
            if (this.userId) {
                if (!id) {
                    this.$root.$emit("onEditPostValidationError", "ID is invalid");
                } else if (!text || text.length < 10) {
                    this.$root.$emit("onEditPostValidationError", "Text is too short");
                } else {
                    let posts = Object.values(this.posts).filter(p => p.id === parseInt(id));
                    if (posts.length) {
                        posts.forEach((item) => {
                            item.text = text;
                        });
                    } else {
                        this.$root.$emit("onEditPostValidationError", "No such post");
                    }
                }
            } else {
                this.$root.$emit("onEditPostValidationError", "No access");
            }
        });

        this.$root.$on("onWriteComment", (userId, postId, text) => {
          if (this.userId) {
            if (!text || text.length < 5) {
              this.$root.$emit("onWritePostValidationError", "Title is too short");
            } else {
              const id = Math.max(...Object.keys(this.comments)) + 1;
              this.$root.$set(this.comments, id, {
                id, userId, postId, text
              });
            }
          } else {
            this.$root.$emit("onWriteCommentValidationError", "No access");
          }
        });
    }


}
</script>

<style>
#app {

}
</style>
