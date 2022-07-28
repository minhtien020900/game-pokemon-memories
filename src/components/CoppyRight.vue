<template>
  <div class="copyright">
    <p>De gio cuon di <a href="#">view here</a></p>
  </div>
</template>

<script>
export default {
  name: "CopyRight",
};
</script>

<style scoped>
.copyright {
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  bottom: 0.5rem;
  color: var(--light);
  z-index: 3;
  font-size: 1.5rem;
}
.copyright a {
  color: #f4dc26;
}
</style>
