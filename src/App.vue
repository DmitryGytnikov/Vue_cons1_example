<script setup>
import { ref } from 'vue'

const users = ref([
  {
    id: 1,
    name: 'Vasya',
  },
  {
    id: 2,
    name: 'Petya',
  },
  {
    id: 3,
    name: 'Masha',
  },
])

const newUsername = ref('')

const deleteUser = (id) => {
  users.value = users.value.filter((user) => user.id !== id)
}

const addUser = () => {
  if (newUsername.value === '') return

  users.value.push({
    id: users.value.length + 1,
    name: newUsername.value,
  })

  newUsername.value = ''
}
</script>

<template>
  <div>ЗНАЧЕНИЕ ТЕКУЩЕЕ ИНПУТА: {{ newUsername }}</div>
  <form @submit.prevent="addUser">
    <label>
      Введите имя
      <input v-model="newUsername" type="text" />
      <button>Добавить</button>
    </label>
  </form>
  <div v-for="user in users" class="user-card">
    <div @click="deleteUser(user.id)">X</div>
    <div class="user-img">{{ user.id }}</div>
    <div class="username">{{ user.name }}</div>
  </div>
</template>

<style scoped>
.user-card {
  display: flex;
  width: 200px;
  height: 300px;
  border: solid 1px black;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 30px;
}

.user-img {
  width: 100%;
  height: 70%;
  border: 1px solid black;
}

.username {
  flex-grow: 1;
  border: 1px solid black;
  width: 100%;
}
</style>
