<template>
  <div id="app" class="main-container">
    <pandoras-box
      caption="Accepting it will open a pandora's box"
      @reject="handleReject"
      @accepted="handleAccept"
    ></pandoras-box>
  </div>
</template>

<script setup lang="ts">
import PandorasBox from "./components/PandorasBox.vue";
function handleReject(): void {
  alert("Rejected to open the pandora's box");
}
function handleAccept(): void {
  alert("You have accepted opening the pandora's box");
}
</script>

<style scoped lang="scss">
#app {
  font-family: "Inter", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #000000;
  box-sizing: border-box;
}
.main-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #1e1e1e;
}
</style>
