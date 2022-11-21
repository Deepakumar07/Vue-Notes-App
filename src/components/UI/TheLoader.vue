<template>
  <div class="spinner-container">
    <div class="spinner-border spinner-size" :class="[`text-${color || 'primary'}`, `fs-${size || null}`]" role="status">
      <span class="visually-hidden">Loading...</span>
    </div>
  </div>
</template>

<script>
export default {
  props: ["color", "size"],
};
</script>

<style scoped>
.spinner-container {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 20;
}
.spinner-size {
  width: 3rem;
  height: 3rem;
}
</style>
