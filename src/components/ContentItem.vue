<template>
  <li
    class="content-item"
    v-bind:class="{ 'content-item--selected': isSelected }"
    v-on:click="clickHandler(item)"
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
    pathToSelected: String,
    selectedId: String

  },
  data: function () {
    return {
      id: undefined
    };
  },

  // в момент создания (открытие папки-родителя) присваиваем уникальный Id
  // для дальнейшего сравнения с пропсами о выделенном файле
  created() {
    this.id = this.item.name + ' ' + Date.now();
  },
  
  // если согласно пропсам, наш элемент сейчас выделен,
  //  при закрытии папки-родителя передаем наверх инфу о снятии выделения
  beforeDestroy() {
    if (this.id === this.selectedId) {
      this.$emit("click-on-content", '', undefined);
    }
  },

  computed: {
    isSelected: function () {
      return this.id === this.selectedId;
    }
  },

  methods: {
    // если в компоненте TreeWrapper не записан ID данного элемента как уже выделенного,
    // то дальше передаем наверх его имя и id для формирования пути и сохранения id,
    // в противном случае это повторный клик по элементу - выделение снимается
    clickHandler(item) {
      if (this.id !== this.selectedId) {
        this.$emit("click-on-content", item.name, this.id);
      } else {
        this.$emit("click-on-content", '', undefined);
      }
    }
  }
}
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
