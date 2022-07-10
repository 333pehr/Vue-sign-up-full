<template>
  <div class="greenAlert" v-if="successful == true">
    <span> you have successfully signed up! </span>
  </div>
  <div class="redAlert" v-else-if="successful == false">
    <span v-if="passProblem"> please confirm your password correctly! </span>
    <span v-else> An error occurred, please try again! </span>
  </div>
  <br>
  <div class="container">
    <h1 class="header">Sign Up</h1>
    <form>
      <div>
        <input
          type="text"
          placeholder="First name"
          v-model="user.Firstname"
          class="nameInput"
          style="margin-right: 5px"
          required
        />
        <input
          type="text"
          placeholder="Last name"
          v-model="user.Lastname"
          class="nameInput"
          required
        />
      </div>
      <br />
      <input
        type="email"
        placeholder="E-mail"
        v-model="user.Email"
        class="mainInput"
        required
      />
      <br />
      <input
        type="password"
        placeholder="Password (should contain 8 characters)"
        v-model="user.Password"
        class="mainInput"
        @keypress="passlength()"
        required
      />
      <br />
      <input
        type="password"
        placeholder="Confirm your password"
        v-model="confirmPass"
        class="mainInput"
        required
      />
      <br />
      <input type="checkbox" v-model="user.privacyChack">
      <span class="policy">I've read and accept the <a @click.prevent="showPrivacyFunc()" class="privacyLink">privacy and policy</a></span>
      <br />
      <br />
      <button @click.prevent="submitData()" class="submitButton">Sign Up</button>
    </form>
  </div>
  <Privacy @ruleAccepted="Accepted()" v-if="showPrivacy"/>
</template>

<script>
import Privacy from "./components/PrivacyVue.vue";
import axios from "axios";
export default {
  name: "App",
  components: {
    Privacy,
  },
  data() {
    return {
      user: {
        Firstname: "",
        Lastname: "",
        Email: "",
        Password: "",
        privacyCheck: false,
      },
      Term: false,
      successful: null,
      confirmPass: '',
      showPrivacy: false,
    };
  },
  methods: {
    submitData() {
      if(this.passValidator() && this.user.Email && this.user.Firstname && this.user.Lastname && this.passlength()){
        axios.post("http://localhost:3000/users", this.user);
        this.successful = true;
        this.passProblem = false;
      }
      else if(!this.passValidator()){
        this.successful = false;
        this.passProblem = true;
      }
      else{
        this.successful = false;
        this.passProblem = false;
      }
    },
    passValidator(){
      if(this.confirmPass === this.user.Password){
        return true;
      }
      else{
        return false;
      }
    },
    passlength(){
      if(this.user.Password.length >= 8){
        return true;
      }
      else{
        return false;
      }
    },
    showPrivacyFunc(){
      this.showPrivacy= true;
    },
    Accepted(){
      this.user.privacyCheck= true;
      this.showPrivacy= false;
    }
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: 'montserrat', sans-serif;
}
#app {
  background-image: url('./assets/3049487.jpg');
  background-size: cover;
  background-attachment: fixed;
  background-position: center;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  justify-content: center;
  display: flex;
  height: 947px;
}
.container {
  margin-top: 150px;
  text-align: center;
  width: 400px;
  height: 600px;
  background-color: rgba(0,0,0,0.1);
  border: 2px solid white;
  border-radius: 15px;
}
.nameInput {
  width: 45%;
  margin-top: 25px;
  margin-bottom: 10px;
  height: 40px;
  border-radius: 10px;
  padding: 0 0 0 10px;
  border: 1px solid white;
  background-color: rgba(0, 0, 0, 0.2);
  color: white;
  font-weight: 600;
  letter-spacing: 0.1px;
  transition: 400ms;
}
.mainInput{
  width: 85%;
  margin-bottom: 30px;
  height: 40px;
  border-radius: 10px;
  padding: 0 0 0 10px;
  border: 1px solid white;
  background-color: rgba(0, 0, 0, 0.2);
  color: white;
  font-weight: 600;
  letter-spacing: 0.1px;
  transition: 400ms;
}
.mainInput:hover,
.nameInput:hover{
  background-color: rgba(0, 0, 0, 0.6);
}
.header{
  margin-top: 30px;
  color: white;
  margin-bottom: 25px;
  letter-spacing: 2px;
}
.submitButton{
  background-color: #FFC107;
  border: 2px solid #FFC107;
  border-radius: 5px;
  color: black;
  font-weight: 600;
  letter-spacing: 1px;
  width: 40%;
  height: 35px;
  transition: 500ms;
  margin-top: 40px;
}
.submitButton:hover{
  background-color: black;
  color: #FFC107;
}
.policy{
  color: white;
  margin-left: 8px;
  font-size: 16px;
}
.greenAlert{
  color:rgb(124,252,0);
  text-align: center;
  margin-top: 25px;
  width: 400px;
  height: 50px;
  background-color: rgba(127,255,0, 0.3);
  padding-top: 15px;
  position: fixed;
  border-radius: 15px;
}
.redAlert{
  color: rgb(255, 49, 49);
  text-align: center;
  margin-top: 25px;
  width: 400px;
  height: 50px;
  background-color: rgb(222, 49, 99, 0.5);
  padding-top: 15px;
  position: fixed;
  border-radius: 15px;
}
.privacyLink{
  text-decoration: underline;
  color: red;
  cursor: pointer;
}
</style>
