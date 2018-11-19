<template>
    <div id="login">
        <div class="column">
          <h1>Log In</h1>
          <input type="text" name="username" v-model="input.username" placeholder="Username" />
          <input type="password" name="password" v-model="input.password" placeholder="Password" />
          <button type="button" v-on:click="login()">Login</button>
        </div>
        <div class="column">
          <h1>Sign Up</h1>
          <input type="text"  v-model="newUser.name" placeholder="Full Name..">
          <input type="text"  v-model="newUser.username" placeholder="Username.." />
          <input type="password" v-model="newUser.password" placeholder="Password.." />
          <input type="text"  v-model="newUser.email" placeholder="Email.." />
          <input type="text"  v-model="newUser.imgUrl" placeholder="Paste imgUrl here.." />
          <button type="button" v-on:click="registerUser()">Registrer</button>
        </div>

    </div>
</template>
<script>

  class User {
    constructor(uid, name, email, imgUrl, password) {
      this.uid = uid; //this.username = username;
      this.name = name;
      this.email = email;
      this.imgUrl = imgUrl;
      this.password = password;
    }
  }

    export default {
        name: 'Login',
        data() {
            return {
                input: {
                    username: "",
                    password: ""
                },
                newUser:{
                  username:"",
                  name:"",
                  email:"",
                  imgUrl:"",
                  password:""
                }
            }
        },
        methods: {
            login() {
                if(this.input.username != "" && this.input.password != "") {
                  for(var i = 0; i<this.$parent.users.length; i++){
                    if(this.$parent.users[i].uid == this.input.username){
                      if(this.$parent.users[i].password == this.input.password){
                        this.$emit("authenticated", true);
                        this.$parent.loggedInUser = this.input.username; //lagrer brukernavn som loggedInUser
                        this.$router.replace({ name: "myprofile", params: {username:this.input.username} });
                      }
                    }
                  }
                } else {
                    console.log("A username and password must be present");
                }
            },
            registerUser(){
              for(var i = 0; i<this.$parent.users.length; i++){
                if(this.$parent.users[i].username == this.newUser.username){
                  alert("Brukernavnet er opptatt, prøv på nytt");
                }
              }
              this.$parent.users.push( new User(
                                                    this.newUser.username,
                                                    this.newUser.name,
                                                    this.newUser.email,
                                                    this.newUser.imgUrl,
                                                    this.newUser.password
                                                  ));
              this.$emit("authenticated", true);
              this.$parent.loggedInUser = this.newUser.username; //lagrer brukernavn som loggedInUser
              this.$router.replace({ name: "myprofile", params: {username:this.newUser.username} });
              alert("GRATULERER MED NY BRUKER");
            }
        }
    }
</script>
<style scoped>
#login{
  display: flex;
  flex-direction: row;
  justify-content: center;
}
  .column{
    display: flex;
    flex-direction: column;
    width:25%;
    margin: 20px;
  }
</style>
