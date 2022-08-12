<template>
  <draggable
    class="node"
    tag="tbody"
    :group="{ name: 'g1' }"
    item-key="name"
    :list="nodes"
  >
    <template #item="{ element }">
      <tr :style="{ 'margin-left': `${depth * 20}px` }">
        <td scope="row">
          <span class="type" @click="nodeClicked(element)">{{
            isExpanded(element) ? "&#9660;" : "&#9658;"
          }}</span
          >{{ element.id }}
        </td>
        <td>{{ element.name }}</td>
        <td>{{ element.sport }}</td>
        <nested-draggable
          v-if="isExpanded(element) && element.children"
          :nodes="element.children"
          :depth="depth + 1"
          @onClick="(element) => $emit('onClick', element)"
        />
      </tr>
    </template>
  </draggable>
</template>
<script>
import draggable from "vuedraggable";

export default {
  name: "nested-draggable",

  components: {
    draggable,
  },
  props: {
    nodes: {
      required: true,
      type: Array,
    },
    depth: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      expanded: [],
    };
  },
  methods: {
    isExpanded(node) {
      return this.expanded.indexOf(node) !== -1;
    },
    nodeClicked(node) {
      if (!this.isExpanded(node)) {
        this.expanded.push(node);
      } else {
        this.expanded.splice(this.expanded.indexOf(node));
      }
    },
  },
};
</script>
<style scoped>
.node {
  text-align: left;
  font-size: 18px;
}
.type {
  margin-right: 10px;
}
</style>
