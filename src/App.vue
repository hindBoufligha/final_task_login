<template>
 <v-app id="app">
    <v-container fluid fill-height>
      <v-layout align-center justify-center>
        <v-flex xs12 sm8 md4>

<!--
          <Login v-on:childToParent="onChildClick" v-on:childToParent2 = "onChildClick2"/>

          <p id="username" label="label">Username: {{this.username}}</p>
          <p id="email" label="label">E-mail: {{this.email}}</p>
          <p id="isStaff" label="label">IsStaff: {{this.is_staff}}</p> 
          <p id="pk" label="label">PK: {{this.pk}}</p>
           
         
-->

          
          <div v-if="is_logged == false">

             <Login v-on:childToParent="onChildClick" v-on:childToParent2 = "onChildClick2"/>
            

          </div>

          <div v-else-if="is_logged == true">

          <p id="username" label="label">Username: {{this.username}}</p>
          <p id="email" label="label">E-mail: {{this.email}}</p>
          <p id="isStaff" label="label">IsStaff: {{this.is_staff}}</p>
          <p id="pk" label="label">PK: {{this.pk}}</p>

          </div> 
          

        </v-flex>
      </v-layout>
    </v-container>
 </v-app>
</template>

<script>
import Login from './components/Login.vue'

export default {
  name: 'App',

  components: {
    Login
  },

  data(){
    return{

      is_logged: false,
      username: '',
      email: '',
      pk: 0,
      is_staff: true


    }
  },



  methods:{

    onChildClick (value) {

      this.username = value.username
      this.email = value.email
      this.pk = value.pk
      this.is_staff = value.is_staff

    },

    onChildClick2 (value) {

      this.is_logged = value

    }

  }
}
</script>

<style>
#app {
  
  /*font-family: Avenir, Helvetica, Arial, sans-serif;*/
  font-family: 'Amaranth', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
 /* margin-top: 60px;*/
}

#username {
  margin-top: 30px;
}
</style>
