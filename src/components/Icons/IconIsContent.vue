<template>
  <span class="icon-is-content">
        {{ isOpen ? "[-]" : "[+]" }}
      </span>
</template>

<script>
export default {
    name: "IconIsContent",
    props: {
    isOpen: Boolean,
  },

}
</script>

<style scoped>
.icon-is-content {
  display: inline-block;
  width: 20px;
}
</style>