<template id="makeBid">
  <form id="pb" class="hidden">
    <label>Make bid:</label>
    <input type="number" :min=parseInt(this.$parent.$parent.products[this.pid].highestBid)+1 v-model="placedBid" @keyup.enter="placeBid"/>
  </form>
</template>

<script>
export default {
  props:{
    bid:String,
    pid:String,
    bidder:String,
  },
  data(){
    return{
      placedBid:''
    }
  },
  methods:{
    placeBid(){
      if(parseInt(this.placedBid) > parseInt(this.$parent.$parent.products[this.pid].highestBid)){
        console.log(this.placedBid + " er større enn "+ this.$parent.$parent.products[this.pid].highestBid);
        if(this.$parent.$parent.products[this.pid].owner == this.$parent.$parent.loggedInUser){
          alert("It's illegal to bid on your own products");
          return;
        }
        if(this.$parent.$parent.products[this.pid].highestBidder == this.$parent.$parent.loggedInUser){
          alert("You already have the highest bid. To bid higher is stupid. You are stupid.");
          return;
        }
        this.$parent.$parent.products[this.pid].highestBid = this.placedBid;
        this.$parent.$parent.products[this.pid].highestBidder = this.$parent.$parent.loggedInUser;
        alert("GRATULERER, du har nå det høyeste budet på "+this.$parent.$parent.products[this.pid].name+" med "+this.placedBid+"kr!")
      }else{
        console.log(this.placedBid + " er mindre enn "+ this.$parent.$parent.products[this.pid].highestBid);
      }
    }
  },
  mounted:function(){
    if(this.$parent.$parent.authenticated==true){
      document.getElementById("pb").classList.add("visible");
    }else{
      document.getElementById("pb").classList.remove("visible");
    }
  }

}

</script>
<style scoped>
.hidden{
  display: none;
}
.visible{
  display: flex;
}
</style>
