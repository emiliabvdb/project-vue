<template>
    <div id="login">
        <div class="column" id="inlog">
          <h1>Log In</h1>
          <input type="text" name="username" v-model="input.username" placeholder="Username" />
          <input type="password" name="password" v-model="input.password" placeholder="Password" />
          <button type="button" v-on:click="login()">Login</button>
          <br>
          <button type="button" v-on:click="showRegister()">Sign up</button>
        </div>
        <div class="column hide" id="newUser">
          <h1>Sign Up</h1>
          <input type="text"  v-model="newUser.name" placeholder="Full Name..">
          <input type="text"  v-model="newUser.username" placeholder="Username.." />
          <input type="password" v-model="newUser.password" placeholder="Password.." />
          <input type="text"  v-model="newUser.email" placeholder="Email.." />
          <input type="text"  v-model="newUser.imgUrl" placeholder="Paste imgUrl here.." />
          <button type="button" v-on:click="registerUser()">Registrer</button>
          <br>
          <button type="button" v-on:click="hideRegister()">Back to login</button>
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
                if(this.$parent.users[i].uid == this.newUser.username){
                  alert("Brukernavnet er opptatt, prøv på nytt");
                  return;
                }
                if(this.newUser.imgUrl==""){
                  this.newUser.imgUrl='https://scontent-arn2-1.xx.fbcdn.net/v/t1.15752-9/46524159_271825636852427_6760347513963675648_n.jpg?_nc_cat=101&_nc_ht=scontent-arn2-1.xx&oh=b6c9c599be532e9e007c76edb1bc36c8&oe=5CAC3A81'
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
            },
            showRegister(){
              document.getElementById("newUser").classList.add("visible");
              document.getElementById("inlog").classList.add("hide");
            },
            hideRegister(){
              document.getElementById("newUser").classList.remove("visible");
              document.getElementById("inlog").classList.remove("hide");
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
  .hide{
    display: none;
  }
  .visible{
    display: flex;
  }
</style>
