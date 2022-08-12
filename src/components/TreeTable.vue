<template>
  <div class="row">
    <h1>Tree</h1>
    <table>
      <thead>
        <tr>
          <th scope="col">Id</th>
          <th scope="col">Name</th>
          <th scope="col">Sport</th>
        </tr>
      </thead>

      <nested-draggable :nodes="list" @onClick="nodeWasClicked" />
    </table>
  </div>
</template>

<script>
import nestedDraggable from "./nestedDraggable.vue";
export default {
  components: {
    nestedDraggable,
  },
  data() {
    return {
      list: [
        { id: 1, name: "Abby", sport: "basket" },
        {
          id: 2,
          name: "Brooke",
          sport: "foot",
          children: [
            { id: 7, name: "jack", sport: "foot" },
            {
              id: 8,
              name: "mike",
              sport: "volley",
              children: [
                { id: 9, name: "yao", sport: "foot" },
                { id: 10, name: "sell", sport: "volley" },
              ],
            },
          ],
        },
        { id: 3, name: "Courtenay", sport: "volley" },
        { id: 4, name: "David", sport: "rugby" },
      ],
    };
  },
  methods: {
    nodeWasClicked(node) {
      alert(node.name);
    },
  },
};
</script>

<style lang="scss" scoped></style>
