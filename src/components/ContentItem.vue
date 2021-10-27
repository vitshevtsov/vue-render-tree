<template>
  <li
    class="content-item"
    v-bind:class="{ 'content-item--selected': isSelected }"
    v-on:click="selectHandler(item)"
  >
    <span> {{ item.type === "file" ? "&#128196;" : "&#128225;" }}</span>
    {{ item.name }}
  </li>
</template>

<script>
export default {
  name: "ContentItem",
  props: {
    item: Object,
    selected: Object,
  },
  computed: {
    isSelected() {
      return this.selected === this.item;
    },
  },

  methods: {
    
    // если в компоненте TreeWrapper не записан наш элемент как уже выделенный,
    // то дальше передаем наверх его и его имя для формирования пути
    selectHandler(item) {
      if (this.selected !== item) {
        this.$emit("click-on-content", item, item.name);
      } else {
        this.$emit("click-on-content", {}, "");
      }
    },
  },
};
</script>

<style scoped>
.content-item {
  margin-left: 20px;
  cursor: default;
}

.content-item--selected {
  background-color: aquamarine;
}
</style>