<template>
  <div class="tree">
    <ul class="tree-list">
      <node-tree :node="treeData"></node-tree>
    </ul>
  </div>
</template>

<script>
import NodeTree from "./NodeTree.vue";

export default {
  props: {
    treeData: Object,
  },components: {
    NodeTree,
  },
};
</script>

<style>
.tree {
  padding: 1rem;
  border-top-right-radius: 10px;
  border-bottom-right-radius: 10px;
  box-shadow: 2px 3px 10px rgba(0, 0, 0, 0.2);
  background: #fff;
  max-width: 500px;
  width: 100%;
  overflow: auto;
  margin-right: 20px;
}

li {
  padding-left: 25px;
}
</style>

