<template>
  <b-container class="bv-example-row mt-3 text-center">
    <h3 class="underline-hotpink"><b-icon icon="journals"></b-icon> Board Service</h3>
    <div id="view">
    <transition name="moveInUp">
    <router-view style="margin-top: 30px;"/>
    </transition>
    </div>
  </b-container>
</template>
<script>
export default {
  name: "AppBoard",
};
</script>
<style scoped>
.bv-example-row{
  height: 100vw;
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
#view {
  width: 100vw;
  height: 100vw;
  margin-left: calc(-50vw + 50%);
}
.underline-hotpink {
  display: inline-block;
  background: linear-gradient(180deg, rgba(255, 255, 255, 0) 70%, rgba(231, 27, 139, 0.3) 30%);
}
</style>
