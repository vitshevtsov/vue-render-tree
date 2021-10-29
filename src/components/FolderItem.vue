<template>
  <li>
    <div 
      class="folder-wrapper"
      v-on:click="isOpen = !isOpen"
    >
      <icon-is-content
        v-bind:isOpen="isOpen"
        v-if="hasContent"
      />
      <div class="folder-wrapper_empty">
        <span>&#128194;</span>
        <span>{{ item.name }}</span>
      </div>
    </div>
    <ul 
      v-if="isOpen" 
    >
      <div 
        v-for="(child, index) in item.contents" 
        :key="index">
          <folder-item
            v-if="child.type === 'directory'"
            :pathToSelected="pathToSelected"
            :selectedId="selectedId"
            v-bind:item="child"
            v-on:click-on-content="clickHandler"
          />
          <content-item
            v-else
            :pathToSelected="pathToSelected"
            :selectedId="selectedId"
            v-bind:item="child"
            v-on:click-on-content="clickHandler"
          />
      </div>
    </ul>
  </li>
</template>

<script>
import ContentItem from "./ContentItem.vue";
import IconIsContent from './Icons/IconIsContent.vue';
export default {
  name: "FolderItem",
  props: {
    item: Object,
    pathToSelected: String,
    selectedId: String
  },
  components: {
    ContentItem,
    IconIsContent,
  },
  data: function () {
    return {
      isOpen: false,
    };
  },
  computed: {
    hasContent: function () {
      return this.item.contents.length !== 0;
    },
  },
  methods: {

    // формируем путь к выделенному файлу и передаем наверх вместе с его ID
    clickHandler(selectedName, selectedId) {
        this.$emit(
          "click-on-content",
          this.item.name + " / " + selectedName,
          selectedId
        );
    }
  }
};
</script>

<style scoped>
ul {
  list-style-type: none;
}

li {
  display: inline-block;
}

.folder-wrapper {
  cursor: pointer;
}

.folder-wrapper_empty {
  display: inline-block;
  box-sizing: border-box;
}

</style>
