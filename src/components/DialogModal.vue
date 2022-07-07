<template>
  <div class="container">
    <div class="sub-container">
      <span class="modal-title">{{ title }}</span>
      <div><slot></slot></div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    title: {
      required: true,
      type: String,
    },
  },
};
</script>

<style scoped>
.container {
  border: 1px solid white;
  border-radius: 2rem;
  margin: 0 auto;
  width: 30%;

  background-color: white;
}
.sub-container {
  padding: 20px;
}
.modal-title {
  text-transform: uppercase;
  font-size: 25px;
  font-weight: 400;
}
</style>
