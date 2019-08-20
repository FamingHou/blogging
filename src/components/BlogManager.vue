<template>
  <div>
    <h1>{{ msg }}</h1>
    <el-button @click="drawer = true" type="primary" style="margin-left: 16px;">open</el-button>

    <el-drawer title="I'm the list of posts written by one user" :visible.sync="drawer" size="50%">
      <div>
        <el-button @click="innerDrawer = true">Click me!</el-button>
        <el-table :data="gridData" border stripe>
          <el-table-column property="name" label="Name" width="200"></el-table-column>
          <el-table-column property="email" label="Email"></el-table-column>
        </el-table>
        <el-drawer
          title="I'm the details of one post"
          :append-to-body="true"
          :visible.sync="innerDrawer"
        >
          <p>_(:зゝ∠)_</p>
        </el-drawer>
      </div>
    </el-drawer>
  </div>
</template>

<script>
export default {
  name: "BlogManager",
  props: {
    msg: String
  },
  data() {
    return {
      drawer: false,
      innerDrawer: false,
      gridData: [
        {
          name: "Leanne Graham",
          email: "Sincere@april.biz"
        },
        {
          name: "Ervin Howell",
          email: "Shanna@melissa.tv"
        },
        {
          name: "Clementine Bauch",
          email: "Nathan@yesenia.net"
        }
      ]
    };
  }
};
</script>
