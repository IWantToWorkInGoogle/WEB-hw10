<template>
    <div class="enter form-box">
        <div class="header">Enter</div>
        <div class="body">
            <form @submit.prevent="onEnter">
                <div class="field">
                    <div class="name">
                        <label for="login">Login</label>
                    </div>
                    <div class="value">
                        <input autofocus id="login" name="login" v-model="login"/>
                    </div>
                </div>
                <div class="field">
                    <div class="name">
                        <label for="password">Password</label>
                    </div>
                    <div class="value">
                        <input id="name" name="name" type="name" v-model="name"/>
                    </div>
                </div>
                <div class="field error">{{ error }}</div>
                <div class="button-field">
                    <input type="submit" value="Enter">
                </div>
            </form>
        </div>
    </div>
</template>

<script>
export default {
    name: "Enter",
    data: function () {
        return {
            login: "",
            name: "",
            error: ""
        }
    },
    methods: {
        onEnter: function () {
            this.$root.$emit("onEnter", this.login, this.name);
        }
    },
    beforeCreate() {
        this.$root.$on("onEnterValidationError", (error) => this.error = error);
    }
}
</script>

<style scoped>

</style>