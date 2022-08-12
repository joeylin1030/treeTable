<template>
  <el-card class="tree-card">
    <div class="tree-head">
      <div class="tree-head-one">ID</div>
      <div style="flex: 1; display: flex">
        <div class="tree-head-two">姓名</div>
        <div class="tree-head-three">描述</div>
        <div class="tree-head-three">操作</div>
      </div>
    </div>
    <el-tree
      :data="data"
      draggable
      default-expand-all
      node-key="id"
      ref="treeTable"
      @click="onClickTree"
    >
      <template v-slot="{ node, data }">
        <span class="tree-custom-node">
          <span style="flex: 1">{{ node.label }}</span>
          <span style="flex: 1; display: flex">
            <span type="text" size="mini" style="flex: 1">
              {{ data.label1 }}
            </span>
            <span type="text" size="mini" style="flex: 1">
              {{ data.label2 }}
            </span>
            <span type="text" size="mini" style="flex: 1">
              <span @click.stop="editItem(node)">編輯</span>
              <span @click.stop="deleteItem(node)">刪除</span>
            </span>
          </span>
        </span>
      </template>
    </el-tree>
  </el-card>
</template>

<script>
export default {
  data() {
    return {
      data: [
        {
          id: 1,
          label: "Level one 1",
          label1: "Level one 2",
          label2: "Level one 3",
          children: [
            {
              label: "Level two 1-1",
              label1: "Level one 2",
              label2: "Level one 3",
              children: [
                {
                  label: "Level three 1-1-1",
                  edit: "編輯",
                  delete: "刪除",
                  isShow: true,
                },
              ],
            },
          ],
        },
        {
          label: "Level one 2",
          children: [
            {
              label: "Level two 2-1",
              children: [
                {
                  label: "Level three 2-1-1",
                },
              ],
            },
            {
              label: "Level two 2-2",
              children: [
                {
                  label: "Level three 2-2-1",
                },
              ],
            },
          ],
        },
        {
          label: "Level one 3",
          children: [
            {
              label: "Level two 3-1",
              children: [
                {
                  label: "Level three 3-1-1",
                },
              ],
            },
            {
              label: "Level two 3-2",
              children: [
                {
                  label: "Level three 3-2-1",
                },
              ],
            },
          ],
        },
      ],
      trrDefaultProps: {
        children: "children",
        label: "label",
      },
      treeSelArr: [],
      treeLength: 0,
    };
  },
  methods: {
    onClickTree() {
      this.treeSelArr = [];
      this.treeSelArr = this.$refs.treeTable.getCheckedNodes();
    },
    initTreeLength(arr) {
      let count = 0;
      arr.map((item) => {
        if (item.children) {
          count += item.children.length;
        }
      });
      this.treeLength = count + arr.length;
    },
    editItem(e) {
      console.log(e);
    },
    deleteItem(e) {
      console.log(e);
      const index = this.data.indexOf(e.data);
      console.log(index);
    },
  },
};
</script>
<style scoped>
.tree-card {
  height: 100%;
  background-color: #fff;
  padding: 27px 23px;
}
.tree-card .el-card__body {
  padding: 0;
}
.tree-head {
  background-color: #f8f8f8;
  line-height: 40px;
  height: 40px;
  border: 1px solid #dcdee3;
  border-bottom: none;
  display: flex;
  font-size: 14px;
  color: #606266;
  padding-right: 8px;
}

.tree-head-one,
.tree-head-two,
.tree-head-three {
  flex: 1;
}
.tree-head-one {
  padding-left: 8px;
}
.tree-custom-node {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: 14px;
  padding-right: 8px;
}

.el-tree {
  overflow: hidden;
  border-bottom: 1px solid #dcdee3;
}

.el-tree .el-tree-node {
  border: 1px solid #dcdee3;
  border-bottom: none;
}
.el-tree-node__children .el-tree-node {
  border: none;
}
.el-tree-node__content {
  line-height: 40px !important;
  height: 40px !important;
}

.el-tree-node__children .el-tree-node__content {
  border-top: 1px solid #dcdee3;
}
.el-tree-node:focus > .el-tree-node__content {
  background-color: #fff !important;
}
</style>
