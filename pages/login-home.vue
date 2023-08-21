<template>
        <div class="bg-login login-bg">
            <div class="login-screen">
                <img src="~/assets/images/logo-main.png">
                <router-link to="/staff-login">Login Pentadbir</router-link>
                <router-link to="/employer-login">Login Pengguna</router-link>
                <!-- <router-link to="/modules/faq/faq-list" target="_blank">Frequently Asked Questions</router-link> -->
            </div>
        </div>
</template>
<script>
export default {
    name: "login-home",
};
</script>
