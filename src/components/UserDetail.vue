<template>
  <div class="modal" v-if="show">
    <div class="modal-content">
      <span class="close" @click="$emit('close')">&times;</span>
      <div class="user-info">
        <img :src="user.image" alt="User Image" class="user-image"/>
        <ul>
          <li><strong>ID:</strong> {{ user.id }}</li>
          <li><strong>First Name:</strong> {{ user.firstName }}</li>
          <li><strong>Last Name:</strong> {{ user.lastName }}</li>
          <li><strong>Age:</strong> {{ user.age }}</li>
          <li><strong>Gender:</strong> {{ user.gender }}</li>
          <li><strong>Email:</strong> {{ user.email }}</li>
          <li><strong>Phone:</strong> {{ user.phone }}</li>
          <li><strong>Username:</strong> {{ user.username }}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    user: Object,
    show: Boolean
  }
};
</script>

<style>
.modal {
  display: flex;
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgb(0,0,0);
  background-color: rgba(0,0,0,0.4);
  justify-content: center;
  align-items: center;
}

.modal-content {
  background-color: #fefefe;
  margin: auto;
  padding: 20px;
  border: 1px solid #888;
  width: 80%;
  max-width: 600px;
  border-radius: 10px;
  box-shadow: 0 5px 15px rgba(0,0,0,0.3);
}

.close {
  color: #aaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
  cursor: pointer;
}

.close:hover,
.close:focus {
  color: black;
  text-decoration: none;
  cursor: pointer;
}

.user-info {
  text-align: left;
}

.user-image {
  max-width: 100px;
  margin-bottom: 15px;
}

.user-info ul {
  list-style-type: none;
  padding: 0;
}

.user-info li {
  margin-bottom: 10px;
}
</style>

