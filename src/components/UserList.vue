<template>
    <div>
      <table v-if="users.length" class="user-table">
        <thead>
          <tr>
            <th>ID</th>
            <th>Name</th>
            <th>Gender</th>
            <th>Email</th>
            <th>Age</th>
            <th>Role</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="user in users" :key="user.id">
            <td>{{ user.id }}</td>
            <td>{{ user.firstName }} {{ user.lastName }}</td>
            <td>{{ user.gender }}</td>
            <td>{{ user.email }}</td>
            <td>{{ user.age }}</td>
            <td>{{ user.role }}</td>
            <td><button @click="viewUser(user.id)">View Details</button></td>
          </tr>
        </tbody>
      </table>
      <p v-else>Loading users...</p>
      <UserDetail v-if="selectedUser" :user="selectedUser" @close="selectedUser = null" />
    </div>
  </template>
  
  <style>
  .user-table {
    width: 100%;
    border-collapse: collapse;
    margin: 20px 0;
    font-size: 16px;
    text-align: left;
  }
  .user-table thead tr {
    background-color: #f2f2f2;
    color: #333;
    font-weight: bold;
  }
  .user-table th,
  .user-table td {
    padding: 12px 15px;
    border: 1px solid #ddd;
  }
  .user-table tbody tr:nth-child(even) {
    background-color: #f9f9f9;
  }
  .user-table tbody tr:hover {
    background-color: #f1f1f1;
  }
  button {
    background-color: #4CAF50;
    color: white;
    padding: 10px 15px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  button:hover {
  background-color: #800080; 
}

  </style>
  
  
  <script>
import axios from 'axios';
import UserDetail from './UserDetail.vue';

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
        const response = await axios.get('https://dummyjson.com/users');
        this.users = response.data.users;
      } catch (error) {
        console.error('Failed to fetch users:', error);
      }
    },
    async viewUser(id) {
      try {
        const response = await axios.get(`https://dummyjson.com/users/${id}`);
        this.selectedUser = response.data;
      } catch (error) {
        console.error('Failed to fetch user details:', error);
      }
    },
  },
  mounted() {
    this.fetchUsers();
  },
};
</script>
