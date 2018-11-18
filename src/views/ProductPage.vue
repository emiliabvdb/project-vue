<template>
  <div id="product">
    <img :src="$route.params.imgUrl" />
    <div class="info">
      <h1>{{$route.params.pname}}</h1>
      <p><b>Owner: </b>{{$route.params.owner}}</p>
      <p><b>Highest bid: </b>{{$route.params.highestBid}}</p>
      <p><b>End time: </b>{{$route.params.timeout}}</p>
      <Countdown :end=$route.params.timeout></Countdown>
    </div>

  </div>
</template>

<script>
  import Countdown from 'vuejs-countdown';

  export default {
    name: 'product',
    components: {
      Countdown
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

</style>
