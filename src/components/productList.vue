<template>
      <div class="product">
        <img :src=imgUrl ></img>
        <div class="info">
          <p><b>Name:</b> {{name}}</p>
          <p><b>Owner:</b> {{owner}}</p>
          <p><b>highestBid:</b> {{highestBid}}</p>
          <b>Time left: </b> <Countdown :end=timeout></Countdown>
          <br>
          <router-link :to="{ name: 'product', params: {pname: name, owner: owner, highestBid: highestBid, timeout:timeout, imgUrl: imgUrl } }">more..</router-link>
        </div>
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
      return this.productList.filter((product) => {
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

</style>
