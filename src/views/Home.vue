<template>
  <div class="home">
    <div class="search-wrapper">
      <label>Search title:</label>
      <input type="text" v-model="$parent.search" placeholder="Search title.."/>
    </div>
    <div class="wrapper">
       <div class="card" v-for="product in $parent.filteredList"> <!-- :key="product.pid"> -->
        <productPreview :name=product.name :owner=product.owner :highestBid=product.highestBid :timeout=product.timeout :imgUrl=product.imgUrl :pid=product.pid :highestBidder=product.highestBidder ></productPreview>
       </div>
    </div>
    <br>
  </div>
</template>

<script>
// @ is an alias to /src
import productPreview from "@/components/productPreview.vue";



export default {
  name: "home",
  components: {
    productPreview
  },
  data () {
    return {
      search: '',
      title: 'Products'

    }
  }
};

</script>
