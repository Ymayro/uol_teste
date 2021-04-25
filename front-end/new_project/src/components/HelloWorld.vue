<template>
  <div class="wrapper">
    <h3>Usuários</h3>
    Nome<input type="text" v-model="user"/>
    <button type="button" @click="setUser">Inserir</button>
    <ul >
      <div v-for="(user, index) in userList" :key="index"> 
      <li>{{user.name}}</li>
      <button type="button" @click="deleteUser(user.id)">Excluir</button>
      </div>
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
      user: null,
      userList: []
    }
  },
  methods: {
    getUsers(){
      axios.get('/users')
      .then((response) => {
        this.userList = response.data
      }).catch(e => {
        this.userList = e
      })
    },
    setUser(){
      let newId = this.userList[this.userList.length - 1].id + 1
      let data = {
        id: newId,
        name: this.user
      }
      axios.post('/users', data)
      .then((response) => {
        console.log(response.data)
        this.getUsers()
        this.user = null
      }).catch(e => {
        console.log(e)
      })
    },
    deleteUser(id){
      axios.delete('/users/' + id)
      .then((response) => {
        console.log(response.data);
        this.getUsers()
      }).catch(e => {
        console.log(e)
      })
    }
  },
  beforeMount(){
    this.getUsers()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.wrapper{
  background-color: #0FE6F4;
  position: absolute;
  width: 70%;
  height: 70%;
  overflow-y: scroll;
  top: 10%;
  left: 15%;
}
</style>
