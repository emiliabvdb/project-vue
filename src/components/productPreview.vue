<template>
  <div class="">
    <router-link :to="{ name: 'product', params: {pname: name, owner: owner, highestBid: highestBid, highestBidder: highestBidder, timeout: timeout, imgUrl: imgUrl, pid:pid } }">
      <div class="product">
        <img :src=imgUrl ></img>
        <div class="info">
          <p><b>Name:</b> {{name}} </p>
          <p><b>Owner:</b> {{prodOwnerName}}</p>
          <p><b>Highest Bid:</b> {{highestBid}}$ by {{highestBidderName}} </p>
          <b>Time left: </b> <Countdown :end=timeout></Countdown>

        </div>
        <Countdown class="hide" :end=timeout></Countdown>
      </div>
    </router-link>
  </div>
</template>

<script>
import Countdown from 'vuejs-countdown';


export default {
  props: {
    name: String,
    pid:String,
    owner: String,
    highestBid: String,
    highestBidder: String,
    timeout: String,
    imgUrl: String

  },
  components: {
    Countdown
  },
  computed:{
    prodOwnerName(){
      for(var i = 0; i <this.$parent.$parent.users.length; i++ ){
        if(this.$parent.$parent.users[i].uid == this.owner){
          return this.$parent.$parent.users[i].name;
        }
      }
    },
    highestBidderName(){
      for(var i = 0; i<this.$parent.$parent.users.length; i++){
        if(this.$parent.$parent.users[i].uid == this.highestBidder){
          return this.$parent.$parent.users[i].name;
        }
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

a {
  color: #2c3e50;
  text-decoration: none;
}
.product {
  background-color: lightgreen;
  display: flex;
  flex-direction: row;
  margin: 40px;
}
img{
  width: 200px;
  height: 200px;
  margin: 20px;
  object-fit: cover
}

.info{
  text-align: left;
}

.hide{
  visibility: hidden;
}

</style>
