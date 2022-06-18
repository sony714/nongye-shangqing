<template>
  <div id="app">
    <Base />
  </div>
</template>

<script>
import Base from "@/components/Base.vue";
const width = document.documentElement.clientWidth;
const height = document.documentElement.clientHeight;
document.documentElement.style.fontSize = `${width/100}px`
export default {
  name: "App",
  components:{
    Base
  },
 mounted(){
  
 }
};
</script>

<style>
*{
    margin:0;
    padding: 0;
}
h1,h2,h3,ul,li{
    color:#fff;
}

ul,ol{
    list-style: none;
}

body{
    background: url(../src/assets/image/bg2.png) no-repeat top center;
    line-height: 1.15;
}
</style>
