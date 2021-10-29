<template>
  <div>
    <div class="path-wrapper"><b>Path to selected file:</b> {{ pathToSelected }}</div>
    <folder-item
      :item="item"
      :pathToSelected="pathToSelected"
      :selectedId="selectedId"
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
  
  // храним здесь путь к текущему выделенному файлу / ссылке, и его ID
  data: function () {
    return {
      pathToSelected: '',
      selectedId: undefined
    };
  },
  methods: {
    
    // метод принимает путь к выделенному файлу / ссылке, и его ID
    clickOnContent(pathToSelectedEl, selectedElId) {
        this.pathToSelected = pathToSelectedEl;
        this.selectedId = selectedElId;
        if (this.selectedId === undefined) this.pathToSelected = '';
    },
  },
};
</script>

<style scoped>
.path-wrapper {
    margin-bottom: 20px;
    padding-left: 20px;;
    min-height: 50px;
    display: flex;
    align-items: center;
    border: #2c3e50 2px solid;
}
</style>
