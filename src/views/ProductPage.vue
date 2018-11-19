<template>
  <div id="product">
    <img :src=$route.params.imgUrl />
    <div class="info">
      <h1>{{$route.params.pname}}</h1>
      <p><b>Owner: </b>{{prodOwnerName}}</p>
      <p><b>Highest bid: </b>{{this.$parent.products[$route.params.pid].highestBid}}</p>
      <p><b>By: </b>{{highestBidderName}}</p>
      <p><b>End time: </b>{{$route.params.timeout}}</p>
      <Countdown :end=$route.params.timeout></Countdown>

      <br>
      <makeBid :bid=$route.params.highestBid :pid=$route.params.pid :bidder=this.$parent.$parent.loggedInUser />
    </div>

    <Countdown class="hide" :end=$route.params.timeout></Countdown>
  </div>
</template>

<script>
  import Countdown from 'vuejs-countdown';
  import makeBid from '@/components/makeBid.vue';

  export default {
    name: 'product',
    data (){
      return{
        bid:''
      }
    },
    props:{
      end: String
    },
    components: {
      Countdown,
      makeBid
    },
    computed:{
      prodOwnerName(){
        for(var i = 0; i <this.$parent.users.length; i++ ){
          if(this.$parent.users[i].uid == this.$parent.products[this.$route.params.pid].owner){
            return this.$parent.users[i].name;
          }
        }
      },
      highestBidderName(){
        for(var i = 0; i<this.$parent.users.length; i++){
          if(this.$parent.users[i].uid == this.$parent.products[this.$route.params.pid].highestBidder){
            return this.$parent.users[i].name;
          }
        }
      }

    }

  };

</script>

<style scoped>
  #product{
    width: 90%;
    display: flex;
    flex-direction: row;
    border: 1px solid lightgrey;
  }
  img{
    width: 350px;
    height: 350px;
    background-color: grey;
    margin: 20px;
    object-fit: cover;
  }
  .info{
    text-align: left;
  }
  .hide{
    visibility: hidden;
  }

</style>
