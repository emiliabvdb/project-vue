<template>
  <div class="home">
    <navigation></navigation>
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>

    <heiWorld msg="Welcome to Your life"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import Navigation from "@/components/navigation.vue";
import heiWorld from "@/components/heiWorld.vue";


export default {
  name: "home",
  components: {
    HelloWorld,
    Navigation,
    heiWorld
  }
};

</script>
