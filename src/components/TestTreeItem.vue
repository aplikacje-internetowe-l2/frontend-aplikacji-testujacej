<template>
  <li style="user-select: none; list-style-type: none; text-align: left;">
    <div
        style="display:inline"
        :class="{bold: isFolder}"
        @click="toggle"
    >
      {{ item.value.Name }}
      <span v-if="isFolder">
        <font-awesome-icon v-if="this.item.value.Closed !== true" icon="folder"/>
        <font-awesome-icon v-if="this.item.value.Closed === true" icon="folder-open"/>
      </span>
    </div>
    <ul style="padding-left: 5px" v-show="this.item.value.Closed" v-if="isFolder">
      <test-tree-item
          class="item"
          v-for="(child, index) in item.children"
          :key="index"
          :item="child"
      ></test-tree-item>
    </ul>
  </li>
</template>

<script>
import jQuery from 'jquery';

window.$ = window.jQuery = jQuery;

export default {
  components: {
    TestTreeItem: () => import('./TestTreeItem.vue')
  },
  props: {
    item: Object
  },
  data() {
    return {
      isOpen: false
    }
  },
  computed: {
    isFolder: function () {
      return this.item.children && this.item.children.length;
    }
  },
  methods: {
    toggle: function () {
      if (this.isFolder) {
        this.item.value.Closed = !this.item.value.Closed;
      }
    }
  }
}
</script>

<style>
.bold {
  cursor: pointer;
  font-weight: bold;
}
</style>