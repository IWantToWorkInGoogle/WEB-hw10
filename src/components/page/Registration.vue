<template>
      <div class="registration form-box">
            <div class="header">Registration</div>
            <div class="body">
                  <form @submit.prevent="onRegistration">
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
                                    <label for="name">Name</label>
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
    name: "Registration",
    data: function () {
        return {
            login: "",
            name: "",
            error: ""
        }
    },
    methods: {
        onRegistration: function () {
            this.error = "";
            this.$root.$emit("onRegistration", this.login, this.name);
            this.$root.$emit("onChangePage", "Enter");
        }
    },
    beforeMount() {
        this.$root.$on("onRegistrationValidationError", (error) => this.error = error);
    }
}
</script>

<style scoped>

</style>