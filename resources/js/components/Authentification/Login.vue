<template>
    <div class="col-md-8">
        <div class="card card-container">
            <h3>
                Si vous ne disposez pas d'un compte passez à la creation
                <router-link to="/register"> register </router-link>
            </h3>
            <h2>Connexion</h2>
            <form @submit.prevent="handleLogin">
                <div class="form-group">
                    <input
                        placeholder="email"
                        type="email"
                        class="form-control"
                        v-model="user.email"
                    />
                </div>
                <div class="form-group">
                    <input
                        placeholder="password"
                        type="password"
                        class="form-control"
                        v-model="user.password"
                    />
                </div>

                <div class="form-group">
                    <button class="btn btn-primary btn-block">Valider</button>
                </div>
            </form>
        </div>
    </div>
</template>
<script>
const API_URL = "http://localhost:8000/api/auth/";
export default {
    name: "Login",
    data() {
        return {
            user: {},
            message: "",
        };
    },
    methods: {
        handleLogin() {
            return this.axios
                .post(API_URL + "login", this.user)
                .then(
                    (response) => (
                        localStorage.setItem(
                            "user",
                            JSON.stringify(response.data)
                        ),
                        this.$router.push({ name: "profile" })
                    )
                )
                .catch((err) => console.log(err));
        },
    },
};
</script>
