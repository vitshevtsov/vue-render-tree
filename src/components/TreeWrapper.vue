<template>
  <div>
    <div class="path-wrapper"><b>Path to selected file:</b> {{ pathToSelected }}</div>
    <folder-item
      :item="item"
      :selected="selected"
      v-on:click-on-content="clickOnContent"
    />
  </div>
</template>

<script>
import FolderItem from "./FolderItem.vue";
export default {
  name: "TreeWrapper",
  components: {
    FolderItem,
  },
  props: {
    item: Object,
  },
  
  // храним здесь выбранный файл / папку, и путь до нее
  data: function () {
    return {
      selected: {},
      pathToSelected: '',
    };
  },
  methods: {
    
    // метод принимает файл-объект, по которому кликнули, и путь до него
    clickOnContent(item, pathToSelectedEl) {
      this.selected = item;
      this.pathToSelected = pathToSelectedEl;
      
      //предполагалось, что это точно очистит путь, если нет выделенных файлов,
    //но пока не работает, где-то косяк
      if (this.selected === {}) this.pathToSelected = '';
    },
  },
};
</script>

<style scoped>
.path-wrapper {
    min-height: 50px;
    display: flex;
    align-items: center;
    border: #2c3e50 2px solid;
}
</style>