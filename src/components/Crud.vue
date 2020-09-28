<template>
    <div>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="#">Lotes</a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item">
            <a class="nav-link" href="create">Create</a>
          </li>
          <li class="nav-item active">
            <a class="nav-link" href="read">Read</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="update">Update</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="delete">Delete</a>
          </li>
        </ul>
      </div>
    </nav>

    <!--Tabela-->
    <div class="container">
      <table class="table">
        <thead>
          <tr>
            <th scope="col">ID</th>
            <th scope="col">Nome</th>
            <th scope="col">Lotes</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in lista" :key="item.id">
            <td>{{ item.id }}</td>
            <td>{{ item.nome }}</td>
            <td>{{ item.lotes }}</td>
            <td>
              <button v-bind:id="item.id" v-on:click="removeitem($event)" class="btn btn-danger">Apagar</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
export default {
  name: 'Crud',

  data() {
    return {
      lista: [],
    };
  },
  mounted() {
    axios
      .get("http://192.168.100.82:8081/api")
      .then((response) => {
        this.lista = response.data;
      })
      
  },
  methods: {
    removeitem: (event) => {
      axios.delete(`http://192.168.100.82:8081/api/${event.currentTarget.id}`).catch((error) => {
        if (!error) {
          window.alert("Apagado");
        } else {
          window.alert("Erro. Tente novamente")
        }
      });
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
