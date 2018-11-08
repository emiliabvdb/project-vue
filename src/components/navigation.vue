<template>
  <div class="nav">
    <h1>{{appName}}</h1>
    <ul class='rowOfButtons'>
      <li>
        hei
      </li>
      <li>
        heii
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'navigation',
    data () {
      return {
        appName: 'Frilia',
        buttons: [
          { text: 'My Profile'},
          { text: 'Items for sale'}

        ]
      }
    }
  };
</script>

<style scoped>
  .nav h1 {
    color: hotpink;
  }
  .rowOfButtons {
    display: flex;
    flex-direction: row;
    padding: 15px, 15px;
    background-color: pink;
    justify-content: space-around;
  }

</style>
