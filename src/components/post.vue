<template>
  <div id="app">
  <div class="search-wrapper">
    <input type="text" v-model="search" placeholder="Search title.."/>
        <label>Search title:</label>
  </div>
  <div class="wrapper">
    <div class="card" v-for="product in filteredList">
      <a>
        <img v-bind:src="product.imgUrl"/>
        <small>Owned by: {{ product.owner }}</small>
        {{ product.name }}
      </a>
    </div>
  </div>
</div>
</template>


<script>
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
  name:'about',
  data() {
    return{
    search: '',
    productList: [
      new Product(
        1,
        'Brukt Jakke',
        'Frida Tryggestad Klockmann',
        2,
        'https://images.finncdn.no/dynamic/960w/2018/9/vertical-5/20/5/129/691/465_136669269.jpg',
        '150',
        2,
        new Date("2018-12-25T12:00:00Z")
      ),
      new Product(
        2,
        'Smykke',
        'Emilia Botnen Van den Bergh',
        1,
        'https://www.gullfunn.no/content/images/thumbs/0003350_smykke-i-solv.jpeg',
        '250',
        1 ,
        new Date("2018-12-02T12:00:00Z")
      )]
  }},
  computed: {
    filteredList() {
      return this.productList.filter(product => {
        return product.name.includes(this.search)
      })
    }
  }
}
  </script>
