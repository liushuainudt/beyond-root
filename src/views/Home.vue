<template>
  <div class="home">
    <img alt="BoC logo" src="../assets/boc-logo.png" width="20%" height="20%">
    <Cmd/>
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from "@/components/HelloWorld.vue";
import Cmd from "@/components/Cmd.vue";

export default {
  name: "home",
  components: {
    Cmd
  }
};
</script>

<style scoped>

</style>

