<template>
  <div class="wrapper">
    <h3>Usuários</h3>
    <input type="text" v-model="user"/>
    <button type="button" @click="setUser">Inserir</button>
    <ul>
      <li>{{name}}</li>
      <button type="button" @click="getUsers">Excluir</button>
    </ul>  
  </div>
</template>

<script>
import axios from '@/axios.js'

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      name: 'my name',
      user: null,
      userList: []
    }
  },
  methods: {
    getUsers(){
      console.log('users')
      axios.get('/user?ID=12345')
      .then(function (response) {
        console.log(response);
      }).catch(e => {
        console.log(e)
      })
    },
    setUser(){

    },
    deleteUser(){

    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.wrapper{
  background-color: #42b983;

}
</style>
