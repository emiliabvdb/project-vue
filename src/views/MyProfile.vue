<template>
  <div class="profilepage">
    <profile/>

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
    computed: {
      ownersList() {
        return this.productPreview.filter(product => {
          return product.owner.toLowerCase().includes(this.name.toLowerCase())
        })
      }
    }
  };


</script>
