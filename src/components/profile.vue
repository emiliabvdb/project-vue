<template>
  <div class="profile">
    <div class="users" v-for="user in $parent.users">
      <!-- <div class="loggedInUser" v-if='$route.params.username==user.uid'> -->
      <div class="card">
        <img :src="user.imgUrl" />
        <div class="info">
          <p><b>Name:</b> {{user.name}}</p>
          <p><b>Email:</b> {{user.email}} </p>
        </div>
      </div>
      <div class="usersproduct">
        <div class="ownerOf">
        <p>Owner of:</p>
        <div  v-for="product in products">
          <div v-if="product.owner==user.uid">
            <productPreview :name=product.name :owner=product.owner :highestBid=product.highestBid :highestBidder=product.highestBidder :timeout= product.timeout :imgUrl=product.imgUrl></productPreview>
          </div>
        </div>
      </div>
      <div class="highestBidOn">
      <p>Have highest bid on:</p>
      <div  v-for="product in products">
        <div v-if="product.highestBidder==user.uid">
          <productPreview :name=product.name :owner=product.owner :highestBid=product.highestBid :highestBidder=product.highestBidder :timeout= product.timeout :imgUrl=product.imgUrl></productPreview>
        </div>
      </div>
      </div>
      </div>
     <!-- </div> -->
    </div>
  </div>
</template>

<script>

import productPreview from "@/components/productPreview.vue";


  export default {
    name: 'profile',
    components: {
      productPreview
    }
  };






</script>

<style scoped>
  .card {
    background-color: lightgreen;
    display: flex;
    flex-direction: row;
    height: 250px;
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
  .rowOfButtons {
    display: flex;
    flex-direction: row;
    padding: 15px, 15px;
    background-color: pink;
    justify-content: space-around;
  }

  .usersproduct{
    display:  flex;
  }
  .highestBidOn{
    width: 50%
  }
  .ownerOf{
    width: 50%
  }
</style>
