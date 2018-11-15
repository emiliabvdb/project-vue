<template>
  <div class="profile">
    <div class="card" v-for="user in users">
      <div v-if="user.id">
      </div>
      <img :src="user.imgUrl" />
      <div class="">
        <p><b>Name:</b> {{user.name}}</p>
        <p><b>Email:</b> {{user.email}} </p>
      </div><br>
    </div>
    <div class="test">
      <img :src="imgurl" />
      <div class = "info">
        <p><b>Name:</b> {{fname + " " + lname}}</p>
        <p><b>Email:</b> {{email}} </p>
        <p><b>Rating:</b> {{rating}}</p>
      </div>
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
    name: 'profile',
    data () {
      return {
        users: [
           new User(
            'emilia',
            'Emilia Botnen Van den Bergh',
            'ebvdb@hvl.no',
            'https://scontent-arn2-1.xx.fbcdn.net/v/t1.0-9/38043185_10155473704291373_4817665254009864192_n.jpg?_nc_cat=102&_nc_ht=scontent-arn2-1.xx&oh=87db07d966b1f4b4f06f78068ad25f2a&oe=5C6C41DF',
            'emilie'
          ),
          new User(
            'frida',
            'Frida Tryggestad Klockmann',
            'ftk@hvl.no',
            'https://www.gullfunn.no/content/images/thumbs/0003350_smykke-i-solv.jpeg',
            'frida'
          )
        ],

        imgurl:'https://scontent-arn2-1.xx.fbcdn.net/v/t1.0-9/38043185_10155473704291373_4817665254009864192_n.jpg?_nc_cat=102&_nc_ht=scontent-arn2-1.xx&oh=87db07d966b1f4b4f06f78068ad25f2a&oe=5C6C41DF',
        fname: 'Emilia Botnen',
        lname: 'Van den Bergh',
        email: 'emiliabvdb@email.no',
        rating: 4.9
      }
    }
  };






</script>

<style scoped>
  .card {
    background-color: lightgreen;
    display: flex;
    flex-direction: row;
    height: 250px;
  }
  img{
    width: 200px;
    height: 200px;
    background-color: grey;
    margin: 20px;
    object-fit: cover
  }

  .info{
    text-align: left;

  }
  .rowOfButtons {
    display: flex;
    flex-direction: row;
    padding: 15px, 15px;
    background-color: pink;
    justify-content: space-around;
  }

</style>
