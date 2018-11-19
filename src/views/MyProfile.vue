<template>
  <div id="pf" class="profilepage hidden">
    <div v-for="user in $parent.theUser">
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

        <div  v-for="product in $parent.products">
          <div v-if="product.owner==user.uid">
            <productPreview :name=product.name :owner=product.owner :highestBid=product.highestBid :timeout=product.timeout :imgUrl=product.imgUrl :pid=product.pid :highestBidder=product.highestBidder ></productPreview>
          </div>
        </div>
      </div>
      <div class="highestBidOn">
      <p>Have highest bid on:</p>
      <div  v-for="product in $parent.products">
        <div v-if="product.highestBidder==user.uid">
          <productPreview :name=product.name :owner=product.owner :highestBid=product.highestBid :timeout=product.timeout :imgUrl=product.imgUrl :pid=product.pid :highestBidder=product.highestBidder ></productPreview>
        </div>
      </div>
      </div>
      </div>
    </div>

  <profile />

  </div>
</template>
<script>

import Profile from "@/components/profile.vue";
import productPreview from "@/components/productPreview.vue";


  export default {
    name: "myprofile",
    components: {
      Profile,
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
.card{
  display: flex;
  flex-direction: row;
  border: 1px solid lightgrey;
}
.info{
  text-align: left;
}
.usersproduct{
  display:  flex;
}
.productPreview {
  display:table-column;
}
.hidden{
  display: none;
}
.visible{
  display:flex;
}
</style>
