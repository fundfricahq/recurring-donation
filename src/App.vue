<template>
  <donate-dialog></donate-dialog>
</template>

<script>
import DonateDialog from "./components/DonateDialog.vue";
export default {
  components: {
    "donate-dialog": DonateDialog,
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
html {
  font-family: "Jost", sans-serif;
}
body {
  margin: 0;
  background-color: black;
}
</style>
