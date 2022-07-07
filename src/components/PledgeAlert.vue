<template>
  <teleport to="body">
    <div></div>
    <dialog open>
      <slot></slot>
    </dialog>
  </teleport>
</template>
<style scoped>
div {
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100%;
  background-color: rgba(0, 0, 0, 0.75);
  z-index: 10;
}
dialog {
  margin: 0;
  position: fixed;
  top: 30vh;
  left: 30%;
  width: 40%;
  z-index: 100;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  overflow: hidden;
  border-radius: 1rem;
  border: none;
  border-color: white;
  padding: 1rem;
  color: #534b4bc2;
  font-size: 17px;
}
</style>
