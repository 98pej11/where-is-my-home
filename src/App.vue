<template>
  <div id="app" style="width:100%">
    <the-header-navbar></the-header-navbar>
    <transition name="moveInUp">
    <router-view/>
    </transition>
  </div>
</template>

<script>
import TheHeaderNavbar from "@/components/TheHeaderNavbar";
export default {
  name: "App",
  components: {
    TheHeaderNavbar,
  },
};
</script>

<style>
@font-face {
    font-family: 'mfont';
    src: url('C:\Users\98pej\Downloads\gwantong07-15-master\gwantong07-15-master\src\assets\NanumSquareNeo-bRg.ttf');
    /* src: url('C:\Users\multicampus\Downloads\gwantong07-15-master\src\assets\강원교육모두.ttf'); */

    font-weight: normal;
    font-style: normal;
}
.moveInUp-enter-active{
  opacity: 0;
  transition: opacity 1s ease-in;
}
.moveInUp-enter-active{
  animation: fadeIn 1s ease-in;
}
@keyframes fadeIn{
  0%{
    opacity: 0;
  }
  50%{
    opacity: 0.5;
  }
  100%{
    opacity: 1;
  }
}
.App {
  text-align: center;
  font-size: 50px;
  font-family: mfont;
}
#app {
  /* width: auto; */
  font-family: mfont;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  /* background: linear-gradient(to right, #000000 0%, #2c3e50 50%, #000000 100%); */
  color: white;
  background-color: #111111;
  height: 100vw;
}
a.router-link-exact-active {
  color: #89bfef;
}

a.router-link-exact-active:hover {
  text-decoration: none;
}
</style>