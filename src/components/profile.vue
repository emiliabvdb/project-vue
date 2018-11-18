<template>
  <div class="profile">
    <div class="users" v-for="user in users">
      <div class="card">
        <img :src="user.imgUrl" />
        <div class="info">
          <p><b>Name:</b> {{user.name}}</p>
          <p><b>Email:</b> {{user.email}} </p>
        </div>
      </div>
      <div class="usersproduct">
      <div class="ownerOf">
        <p>Owner of:</p>
        <div  v-for="product in productPreview">
          <div v-if="product.ownerId==user.uid">
            <productPreview :name=product.name :owner=product.owner :highestBid=product.highestBid :timeout= product.timeout :imgUrl=product.imgUrl></productPreview>
          </div><br>
        </div>
      </div>
     <div class="highestBidOn">
      <p>Have highest bid on:</p>
      <div  v-for="product in productPreview">
        <div v-if="product.highestBidder==user.uid">
          <productPreview :name=product.name :owner=product.owner :highestBid=product.highestBid :timeout= product.timeout :imgUrl=product.imgUrl></productPreview>
        </div><br>
      </div>
     </div>
     </div>
    </div>
    <!-- <div class="test">
      <img :src="imgurl" />
      <div class = "info">
        <p><b>Name:</b> {{fname + " " + lname}}</p>
        <p><b>Email:</b> {{email}} </p>
        <p><b>Rating:</b> {{rating}}</p>
      </div>
    </div> -->
  </div>
</template>

<script>

import productPreview from "@/components/productPreview.vue";

class User {
  constructor(uid, name, email, imgUrl, password) {
    this.uid = uid; //this.username = username;
    this.name = name;
    this.email = email;
    this.imgUrl = imgUrl;
    this.password = password;
  }
}
class Product {
  constructor(pid, name, owner, ownerId, imgUrl, highestBid, highestBidder, timeout) {
    this.pid = pid;
    this.name = name;
    this.owner = owner;
    this.ownerId = ownerId;
    this.imgUrl = imgUrl;
    this.highestBid = highestBid;
    this.highestBidder = highestBidder;
    this.timeout = timeout;
  }
}

  export default {
    name: 'profile',
    components: {
      productPreview
    },
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
            'https://scontent-arn2-1.xx.fbcdn.net/v/t1.0-9/29314875_10210157233919408_2013080888513921024_n.jpg?_nc_cat=110&_nc_ht=scontent-arn2-1.xx&oh=21e376d68b74dc5a36b663e01d9c9195&oe=5C80A7A1',
            'fride'
          )
        ],
        productPreview: [
          new Product(
            1,
            'Brukt Jakke',
            'Frida Tryggestad Klockmann',
            'frida',
            'https://images.finncdn.no/dynamic/960w/2018/9/vertical-5/20/5/129/691/465_136669269.jpg',
            '150',
            'emilia',
            "November 27, 2018"
          ),
          new Product(
            2,
            'Smykke',
            'Emilia Botnen Van den Bergh',
            'emilia',
            'https://www.gullfunn.no/content/images/thumbs/0003350_smykke-i-solv.jpeg',
            '250',
            'frida',
            "December 24, 2018"
          )],

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
  .highestBidOn{
  }
  .ownerOf{
  }
</style>
