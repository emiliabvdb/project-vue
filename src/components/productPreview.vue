<template>
      <div class="product">
        <router-link :to="{ name: 'product', params: {pname: name, owner: owner, highestBid: highestBid, timeout: timeout, imgUrl: imgUrl } }">
        <img :src=imgUrl ></img></router-link>
        <div class="info">
          <p><b>Name:</b> {{name}}</p>
          <p><b>Owner:</b> {{owner}}</p>
          <p><b>highestBid:</b> {{highestBid}}</p>
          <b>Time left: </b> <Countdown :end=timeout></Countdown>
          <p class="underline"><router-link :to="{ name: 'product', params: {pname: name, owner: owner, highestBid: highestBid, timeout: timeout, imgUrl: imgUrl } }">more..</router-link>
          </p>
        </div>
        <Countdown class="hide" :end=timeout></Countdown>
  </div>
</template>

<script>
import Countdown from 'vuejs-countdown';
export default {
  props: {
    name: String,
    owner: String,
    highestBid: String,
    timeout: String,
    imgUrl: String
  },
  components: {
    Countdown
  },
  computed: {
    filteredProducts: function(){
      return this.productPreview.filter((product) => {
        return product.name.match(this.search);
      });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: black;
  text-decoration: none;
}
.product {
  background-color: lightgreen;
  display: flex;
  flex-direction: row;
  height: 250px;
  margin: 40px;
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

.underline{
  text-decoration-line: underline;
}
.hide{
  visibility: hidden;
}

</style>
