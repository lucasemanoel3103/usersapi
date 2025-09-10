<template>
  <div>
    <h2>Registro de usuário!</h2>
    <hr />

    <div class="columns is-centered">
      <div class="column is-half">
        <p>Nome</p>
        <input
          type="text"
          placeholder="Nome do usuário"
          class="input"
          v-model="name"
        />
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
        <button class="button is-primary is-dark" @click="register">
          Cadastrar
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      password: "",
      email: "",
    };
  },
  methods: {
    register() {
      console.log(this.name);
      console.log(this.password);
      console.log(this.email);
    },
  },
};
</script>

<style scoped></style>
