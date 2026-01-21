<template>
  <div class="container">
    <div class="tree">
      <TreeNode
        v-for="node in tree"
        :key="node.name"
        :node="node"
        :selectedNode="selectedNode"
        @select="selectNode"
      />
    </div>

    <NodeDetails
      v-if="selectedNode"
      :node="selectedNode"
      @close="selectedNode = null"
    />
  </div>
</template>

<script setup>
import { ref } from "vue";
import { graphData } from "./data/graphData";
import TreeNode from "./components/TreeNode.vue";
import NodeDetails from "./components/NodeDetails.vue";

const selectedNode = ref(null);

// Convert flat list to tree
const buildTree = (data) => {
  const map = {};
  const roots = [];

  data.forEach(item => {
    map[item.name] = { ...item, children: [] };
  });

  data.forEach(item => {
    if (item.parent) {
      map[item.parent].children.push(map[item.name]);
    } else {
      roots.push(map[item.name]);
    }
  });

  return roots;
};

const tree = buildTree(graphData);

const selectNode = (node) => {
  selectedNode.value = node;
};
</script>

<style>
.container {
  display: flex;
  height: 100vh;
  font-family: Arial, sans-serif;
}

.tree {
  flex: 2;
  padding: 20px;
}
</style>
