<template>
  <li>
    <div>
      <span
        v-if="hasContent"
        v-on:click="isOpen = !isOpen"
        class="open-close-icon"
      >
        {{ isOpen ? "[-]" : "[+]" }}
      </span>
      <div class="folder-wrapper">
        <span>&#128194;</span>
        <span>{{ item.name }}</span>
      </div>
    </div>
    <ul v-if="isOpen">
      <div 
        v-for="(child, index) in item.contents" 
        :key="index">
          <folder-item
            v-if="child.type === 'directory'"
            :selected="selected"
            v-bind:item="child"
            v-on:click-on-content="clickHandler"
          />
          <content-item
            v-else
            :selected="selected"
            v-bind:item="child"
            v-on:click-on-content="clickHandler"
          />
      </div>
    </ul>
  </li>
</template>

<script>
import ContentItem from "./ContentItem.vue";
export default {
  name: "FolderItem",
  props: {
    item: Object,
    selected: Object,
  },
  components: {
    ContentItem,
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

    // если в параметрах пришел выделенный объект, то вторым параметром
    // дальше передаем путь (складываем имена родителей)
    clickHandler(item, selectedName) {
      if (item !== {}) {
        this.$emit(
          "click-on-content",
          item,
          this.item.name + " / " + selectedName
        );
      } else {
        this.$emit("click-on-content", item, "");
      }
    },
  },
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
  display: inline-block;
  box-sizing: border-box;
}

.open-close-icon {
  display: inline-block;
  width: 20px;
  cursor: pointer;
}
</style>
