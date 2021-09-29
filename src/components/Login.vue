<template>
  <div>
    <!--start-->
    <v-card
    elevation="8"
    haped
    shaped>

    <v-row id="vrow">
      <v-col
      id="email"
      cols="12">

      <v-text-field
      v-model="user.email"
      label="E-mail"
      :rules="emailRules"
      required
      outlined
      clearable>
      </v-text-field>

      </v-col>
    </v-row>

    <v-row id="vrow">
      <v-col
      cols="12">
      
      <v-text-field
      v-model="user.password"
      :rules="passwordRules"
      :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
      :type="show1 ? 'text' : 'password'"
      label="Password"
      required
      outlined
      clearable
      @click:append="show1 = !show1">
      </v-text-field>

      </v-col>
    </v-row>

    <v-btn
    id="login-btn"
    elevation="8"
    large
    outlined
    color="primary"
    v-on:click="user_login"
    v-on:keyup="user_login">
    Login
    </v-btn>
    
    </v-card>


    <v-snackbar
      v-model="snackbar"
      :multi-line="multiLine"
      :timeout="snckbar_timeout">

      {{ snackbar_text }}
      
      <template v-slot:action="{ attrs }">

        <v-btn
          color="red"
          text
          v-bind="attrs"
          @click="snackbar = false">

          Close

        </v-btn>
      </template>
    </v-snackbar>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: 'Login',
  data(){
    return{

      login_status: false,
      valid: false,
      key:'',
      user: {
        email: "",
        password: "",
      },
      
      show1: false,

      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+/.test(v) || 'E-mail must be valid',
      ],
      passwordRules: [
        v => !!v || 'Password is required',
      ],

      multiLine: true,
      snackbar: false,
      snackbar_text: ``,
      snckbar_timeout: 2000

    }
  },
  methods:{

    async user_login() {
      await axios
        .post("https://v2202107122785158474.goodsrv.de/api/rest-auth/login/", this.user)
        .then((res) => {

          console.log(res.status);
          console.log(res.data);

          if(res.status == 200) 
          {

            

            this.login_status = true
            this.snackbar_text = "Successfull Login!"
            this.snackbar = true;

            

            let key = res.data.key;
            console.log(key);
            
            axios.get('https://v2202107122785158474.goodsrv.de/api/rest-auth/user/', {
            "headers":{"Authorization": `Token ${key}`}
            })
            .then((res) => {

              
              console.log(res.data)
              this.$emit('childToParent', res.data)
              this.$emit('childToParent2', true)
              
              });

              
          }
        })
        .catch((err) => {

          console.log(err);
          this.login_status = false
          this.snackbar_text = "Failed Login!"
          this.snackbar = true;
          
        });


        
    },

    
  } /*methods-end*/
}
</script>

<style scoped>


#vrow {
  margin-right: 25px;
  margin-left: 25px;
}

#email {
  margin-top: 20px;
}

#login-btn {
  margin-bottom: 20px;
}




</style>
