<template>
  <div id="NewProduct">
    <h1>Sell a product</h1>
    <img :src="imgUrl" />
    <div class="info">
      <input type="text"  v-model="pname" placeholder="Product Name..">
      <input type="number" min="0" v-model="highestBid" placeholder="starting prize">
      <input type="text" v-model="imgUrl" placeholder="Paste imgUrl here">
      <input type="date" v-model="timeout" :min=today>
      <button type="button" v-on:click="publish()">Publish product</button>
    </div>
  </div>

</template>

<script>
//import Product from '@/App.vue';

class Product {
  constructor(pid, name, owner, imgUrl, highestBid, highestBidder, timeout) {
    this.pid = pid;
    this.name = name;
    this.owner = owner;
    this.imgUrl = imgUrl;
    this.highestBid = highestBid;
    this.highestBidder = highestBidder;
    this.timeout = timeout;
  }
}

export default{
  name: 'productFactory',
  data() {
    return{
      imgUrl:'https://image.freepik.com/free-psd/psd-recycled-paper-shopping-bag_30-2095.jpg',
      pname:'',
      highestBid:'',
      timeout: ''
    }
  },
  computed:{
    today(){
      var today = new Date();
      var dd = today.getDate();
      var mm = today.getMonth()+1; //January is 0!
      var yyyy = today.getFullYear();
      if(dd<10){
        dd='0'+dd
      }
      if(mm<10){
        mm='0'+mm
      }
      today = yyyy+'-'+mm+'-'+dd;
      return today;
    }
  },
  methods:{
    publish(){
      if(this.pname==''){
        alert('The product needs a name');
        return
      }
      if(this.timeout == ''){
        alert('You have to set a timeout');
        return
      }
      if(this.highestBid == ''){
        this.highestBid='0';
      }
      if(this.imgUrl == ''){
        imgUrl = 'https://image.freepik.com/free-psd/psd-recycled-paper-shopping-bag_30-2095.jpg';
      }

      var pid = String(this.$parent.$parent.products.length);
      var liu = this.$parent.$parent.loggedInUser;
      var months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      var date = new Date(this.timeout);
      var prettyDate = months[date.getMonth()]+" "+date.getDate()+", "+ date.getFullYear();

      this.$parent.$parent.products.push( new Product(
                                            pid,
                                            this.pname,
                                            liu,
                                            this.imgUrl,
                                            this.highestBid,
                                            'none',
                                            prettyDate
                                          ));


    }
  }
}
</script>

<style scoped>
  #NewProduct {

  }
  img{
    width: 100px;
  }
  .info{
    display: flex;
    flex-direction: column;
  }
</style>
