<template>
  <div id="NewProduct">
    <h2 v-on:click="toggleVisibility()">Add a product for sale  + </h2>
    <div id="prodFac" class="hidden">
      <img v-if="imgUrl == '' " src="https://image.freepik.com/free-psd/psd-recycled-paper-shopping-bag_30-2095.jpg" />
      <img v-else :src="imgUrl" />
      <div class="info">
        <input type="text"  v-model="pname" placeholder="Product Name..">
        <input type="number" min="0" v-model="highestBid" placeholder="starting prize">
        <input type="text" v-model="imgUrl" placeholder="Paste imgUrl here">
        <input type="date" v-model="timeout" :min=tomorrow>
        <button type="button" v-on:click="publish()">Publish product</button>
      </div>
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
      imgUrl:'',
      pname:'',
      highestBid:'',
      timeout: ''
    }
  },
  computed:{
    tomorrow(){
      var tomorrow = new Date();
      tomorrow.setDate(tomorrow.getDate() + 1);
      var dd = tomorrow.getDate();
      var mm = tomorrow.getMonth()+1; //January is 0!
      var yyyy = tomorrow.getFullYear();
      if(dd<10){
        dd='0'+dd
      }
      if(mm<10){
        mm='0'+mm
      }
      tomorrow = yyyy+'-'+mm+'-'+dd;
      return tomorrow;
    }
  },
  methods:{
    toggleVisibility(){
      if(document.getElementById("prodFac").classList.contains("visible")){
        document.getElementById("prodFac").classList.remove("visible")
      }
      else {
        document.getElementById("prodFac").classList.add("visible");
      }
    },
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
        this.imgUrl = 'https://image.freepik.com/free-psd/psd-recycled-paper-shopping-bag_30-2095.jpg';
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
      document.getElementById("prodFac").classList.remove("visible");
      alert("You have published the product");
    }
  }
}
</script>

<style scoped>
  #NewProduct{
    border: 1px solid lightgrey;
    margin: 40px;
    background-color: lightgrey;
  }

  img{
    width: 200px;
    height: 200px;
    object-fit: cover;
    margin: 50px;
  }
  .info{
    display: flex;
    flex-direction: column;
    margin: 50px;
    width: 30%;
    justify-content: space-around;
  }

  .hidden{
    display: none;
  }
  .visible{
    display: flex;
    justify-content: center;
    background-color: white;
  }
  .row{
    flex-direction: row;
  }

</style>
