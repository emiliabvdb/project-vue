<template>
  <div class="home">
    <div class="search-wrapper">
      <input type="text" v-model="search" placeholder="Search title.."/>
          <label>Search title:</label>
    </div>
    <div class="wrapper">
      <div class="card" v-for="product in productPreview">
        <productPreview :name=product.name :owner=product.owner :highestBid=product.highestBid :timeout= product.timeout :imgUrl=product.imgUrl></productPreview>
      </div>
    </div>
    <heiWorld msg="heiWorld"/>
  </div>
</template>

<script>
// @ is an alias to /src
import heiWorld from "@/components/heiWorld.vue";
import productPreview from "@/components/productPreview.vue";

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
  name: "home",
  components: {
    heiWorld,
    productPreview
  },
  data () {
    return {
      search: '',
      title: 'Products',
      productPreview: [
        new Product(
          1,
          'Brukt Jakke',
          'Frida Tryggestad Klockmann',
          2,
          'https://images.finncdn.no/dynamic/960w/2018/9/vertical-5/20/5/129/691/465_136669269.jpg',
          '150',
          2,
          "November 27, 2018"
        ),
        new Product(
          2,
          'Smykke',
          'Emilia Botnen Van den Bergh',
          1,
          'https://www.gullfunn.no/content/images/thumbs/0003350_smykke-i-solv.jpeg',
          '250',
          1 ,
          "December 24, 2018"
        )],
      users: [
         new User(
          1,
          'Emilia Botnen Van den Bergh',
          'ebvdb@hvl.no',
          'https://scontent-arn2-1.xx.fbcdn.net/v/t1.0-9/38043185_10155473704291373_4817665254009864192_n.jpg?_nc_cat=102&_nc_ht=scontent-arn2-1.xx&oh=87db07d966b1f4b4f06f78068ad25f2a&oe=5C6C41DF',
          'emilie'
        ),
        new User(
          2,
          'Frida Tryggestad Klockmann',
          'ftk@hvl.no',
          'https://www.gullfunn.no/content/images/thumbs/0003350_smykke-i-solv.jpeg',
          'frida'
        )
      ]
    }
  },
  computed: {
    filteredList() {
      return this.productPreview.filter(product => {
        return product.name.toLowerCase().includes(this.search.toLowerCase())
      })
    }
  }
};

</script>
