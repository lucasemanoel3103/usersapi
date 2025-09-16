<template>
  <div>
    <h1>Painel Adm</h1>

    <div class="table-container has-text-centered">
      <table class="table is-bordered is-striped is-hoverable is-fullwidth">
        <thead>
          <tr>
            <th>Nome</th>
            <th>E-mail</th>
            <th>Cargo</th>
            <th>Ações</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="user in users" :key="user.id">
            <td>{{ user.name }}</td>
            <td>{{ user.email }}</td>
            <td>{{ processRole(user.role) }}</td>
            <td>
              <router-link :to="{name: 'UsersEdit', params:{id: user.id}}"><button class="button is-primary is-dark" >Editar</button></router-link>   
              <button class="button is-danger is-dark" @click="showModalUser(user.id)">Deletar</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <div :class="{modal: true, 'is-active': showModal}">
      <div class="modal-background"></div>
      <div class="modal-content">
        <div class="card">
          <header class="card-header">
            <p class="card-header-title">Você quer realmente deletar este usuário?</p>
          </header>
          <div class="card-content">
            <div class="content">
                <p>Está opção vai excluir o usuário do sistema para sempre, deseja mesmo seguir com essa opção?</p>
            </div>
          </div>
          <footer class="card-footer">
            <a href="#" class="card-footer-item" @click="hideModal()">Cancelar</a>
            <a href="#" class="card-footer-item" @click="deleteUser()">Sim, quero deletar!</a>
          </footer>
        </div>
      </div>
      <button class="modal-close is-large" aria-label="close" @click="hideModal()"></button>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  created() {
    const req = {
      headers: {
        Authorization: "Bearer " + localStorage.getItem("token"),
      },
    };

    axios
      .get("http://localhost:8686/user", req)
      .then((res) => {
        console.log(res);
        this.users = res.data;
      })
      .catch((err) => {
        console.log(err);
      });
  },

  data() {
    return {
      users: [],
      showModal: false,
      deleteUserId: -1
    };
  },
  methods: {
    processRole(value) {
      if (value == 0) return "Usuário comum";
      if (value == 1) return "Admin";
      return "Desconhecido";
    },
    hideModal(){
        this.showModal = false;
    },
    showModalUser(id){
        this.deleteUserId = id;
        this.showModal = true;
    },
    deleteUser(){

        const req ={
            headers: { 
                 Authorization: "Bearer " + localStorage.getItem("token")
            }
        }

        axios.delete("http://localhost:8686/user/"+this.deleteUserId, req).then(res => {
            console.log(res);
            this.showModal = false;
            this.users = this.users.filter(u => u.id != this.deleteUserId);
        }).catch(err => {
            console.log(err);
            this.showModal = false;
        })
    }
  },
  
};
</script>

<style scoped></style>
