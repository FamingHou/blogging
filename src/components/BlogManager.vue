<template>
  <div>
    <h1>{{ msg }}</h1>

    <el-table :data="users" border stripe @row-click="onUserSelected">
      <el-table-column property="name" label="User Name" width="200"></el-table-column>
      <el-table-column property="email" label="Email"></el-table-column>
    </el-table>

    <el-drawer title="I am the list of posts written by the selected user" :visible.sync="drawer" size="60%">
      <div>
        <el-table :data="postsWrittenBySelectedUser" border stripe @row-click="onPostSelected">
          <el-table-column property="title" label="Title"></el-table-column>
        </el-table>

        <el-drawer
          title="I am the details of one post"
          :append-to-body="true"
          :visible.sync="innerDrawer"
        >
          <div>
            <el-card v-if="selectedPost" class="box-card">
              <div slot="header" class="clearfix">
                <span>Id: {{selectedPost.id}}</span>
                <el-divider></el-divider>
                <span>User Id: {{selectedPost.userId}}</span>
                <el-divider></el-divider>
                <span>Title: {{selectedPost.title}}</span>
                <el-divider></el-divider>
                <span>Body: {{selectedPost.body}}</span>
              </div>
            </el-card>
          </div>
        </el-drawer>
      </div>
    </el-drawer>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "BlogManager",
  props: {
    msg: String
  },
  data() {
    return {
      drawer: false,
      innerDrawer: false,
      users: null,
      selectedUser: null,
      postsWrittenBySelectedUser: null,
      selectedPost: null
    };
  },
  methods: {
    fetchUsers() {
      axios
        .get("https://jsonplaceholder.typicode.com/users")
        .then(response => (this.users = response.data));
    },
    fetchPostsWrittenBySelectedUser(selectedUser) {
      axios
        .get("https://jsonplaceholder.typicode.com/posts")
        .then(
          response =>
            (this.postsWrittenBySelectedUser = response.data.filter(
              x => x.userId === selectedUser.id
            ))
        );
    },
    onUserSelected(row) {
      this.selectedUser = row;
      this.drawer = true;
      this.fetchPostsWrittenBySelectedUser(this.selectedUser);
    },
    onPostSelected(row) {
      this.selectedPost = row;
      this.innerDrawer = true;
    }
  },
  mounted() {
    this.fetchUsers();
  }
};
</script>
