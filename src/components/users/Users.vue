<template>
    <div class="users datatable">
        <div class="caption">User</div>
            <table>
                <thead>
                    <tr>
                        <th>Id</th>
                        <th>Login</th>
                        <th>Name</th>
                    </tr>
                </thead>
                <tbody>
                    <UsersEachUser v-for="user in users" :user="user" :key="user.id"/>
                </tbody>
            </table>
    </div>
</template>

<script>
import UsersEachUser from "./UsersEachUser";

export default {
    name: "Users",
    components: {
        UsersEachUser
    },
    props: ["users"]
}
</script>

<style scoped>

</style>