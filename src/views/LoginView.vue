<template>
  <div>
    <h2>Login</h2>
    <hr />

    <div class="columns is-centered">
      <div class="column is-half">
        <div v-if="error != undefined">
          <div class="notification is-danger">
            {{ error }}
          </div>
        </div>
        <p>E-mail</p>
        <input
          type="email"
          placeholder="email@email.com"
          class="input"
          v-model="email"
        />
        <p>Senha</p>
        <input
          type="password"
          placeholder="******"
          class="input"
          v-model="password"
        />
        <hr />
        <button class="button is-primary is-dark" @click="login">Login</button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      password: "",
      email: "",
      error: null,
    };
  },
  methods: {
    login() {
      axios
        .post("http://localhost:8686/login", {
          password: this.password,
          email: this.email,
        }).then(res => {
          console.log(res);
          localStorage.setItem('token', res.data.token);
          this.$router.push({ name: 'home' });
        }).catch(err => {
         this.error = err.response?.data?.err || 'Erro na requisição. Verifique o servidor.';
        });
    },
  },
};
</script>

<style scoped></style>
