<template>
  <div>
    <ul v-if="users.length">
      <li v-for="user in users" :key="user.id">
        {{ user.firstName }} {{ user.lastName }}
        <button @click="viewUser(user.id)">View Details</button>
      </li>
    </ul>
    <p v-else>Loading users...</p>
    <UserDetail
      v-if="selectedUser"
      :user="selectedUser"
      @close="selectedUser = null" />
  </div>
</template>

<script>
import axios from "axios";
import UserDetail from "./UserDetail.vue";

export default {
  data() {
    return {
      users: [],
      selectedUser: null,
    };
  },
  components: {
    UserDetail,
  },
  methods: {
    async fetchUsers() {
      try {
        const response = await axios.get("https://dummyjson.com/users");
        this.users = response.data.users;
      } catch (error) {
        console.error("Failed to fetch users:", error);
      }
    },
    async viewUser(id) {
      try {
        const response = await axios.get(`https://dummyjson.com/users/${id}`);
        this.selectedUser = response.data;
      } catch (error) {
        console.error("Failed to fetch user details:", error);
      }
    },
  },
  mounted() {
    this.fetchUsers();
  },
};
</script>
