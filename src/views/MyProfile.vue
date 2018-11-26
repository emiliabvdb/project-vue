<template>
  <div id="pf" class="hidden">
    <div v-for="user in $parent.theUser">
      <div class="card">
        <img :src="user.imgUrl" />
        <div class="info">
          <p><b>Name:</b> {{user.name}}</p>
          <p><b>Username:</b> {{user.uid}} </p>
          <p><b>Email:</b> {{user.email}} </p>
        </div>
      </div>
      <div class="usersproduct">

        <div class="ownerOf">
          <productFactory/>
          <h2>Your products for sale:</h2>
          <div  v-for="product in $parent.products">
            <div v-if="product.owner==user.uid">
              <productPreview :name=product.name :owner=product.owner :highestBid=product.highestBid :timeout=product.timeout :imgUrl=product.imgUrl :pid=product.pid :highestBidder=product.highestBidder ></productPreview>
            </div>
          </div>
        </div>
        <div class="highestBidOn">
            <router-link to="/"><div id="bidMore">
            <h2>Bid on more products</h2>
          </div></router-link>
          <h2>Have highest bid on:</h2>
          <div  v-for="product in $parent.products">
            <div v-if="product.highestBidder==user.uid">
              <productPreview :name=product.name :owner=product.owner :highestBid=product.highestBid :timeout=product.timeout :imgUrl=product.imgUrl :pid=product.pid :highestBidder=product.highestBidder ></productPreview>
            </div>
          </div>
        </div>
      </div>

   </div>
  </div>
</template>
<script>

  import productFactory from "@/components/productFactory.vue";
  import productPreview from "@/components/productPreview.vue";


  export default {
    name: "myprofile",
    components: {
      productFactory,
      productPreview
    },
    mounted: function(){
      if(this.$parent.authenticated==true){
        document.getElementById("pf").classList.add("visible");
      }else{
        document.getElementById("pf").classList.remove("visible");
      }

    }
  };


</script>

<style scoped>
  img{
    width: 200px;
    height: 200px;
    background-color: grey;
    margin: 20px;
    object-fit: cover
  }
  a{
    text-decoration: none;
    color: #2c3e50;
  }

  .card{
    display: flex;
    flex-direction: row;
    border: 1px solid lightgrey;
    min-width: 900px;
    margin: 40px;
  }
  .info{
    text-align: left;
  }
  .usersproduct{
    display:  flex;
  }
  .highestBidOn{
    width: 50%;
  }
  .ownerOf{
    width: 50%;
  }
  .hidden{
    display: none;
  }
  .visible{
    display:flex;
  }
  #bidMore{
    border: 1px solid lightgrey;
    margin: 40px;
    background-color: lightgrey;
  }
</style>
