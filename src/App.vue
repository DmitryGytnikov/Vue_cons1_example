<script setup>
import { ref } from "vue"

const users = ref([
	{
		id: 1,
		name: "Vasya",
	},
	// {
	// 	id: 2,
	// 	name: "Petya",
	// },
	// {
	// 	id: 3,
	// 	name: "Masha",
	// },
	// {
	// 	id: 4,
	// 	name: "Sasha",
	// },
	// {
	// 	id: 5,
	// 	name: "Vanya",
	// },
])

const newUsername = ref("")

const deleteUser = id => {
	users.value = users.value.filter(user => user.id !== id)
}

const addUser = () => {
	if (newUsername.value === "") return

	users.value.push({
		id: users.value.length + 1,
		name: newUsername.value,
	})

	newUsername.value = ""
}
</script>

<template>
	<div class="container-wr">
		<div class="container">
			<div class="counter">
				<p>Tasks</p>
				<div>(<span>1</span>)</div>
			</div>
			<div class="create-task">
				<input type="text" />
				<button>Add</button>
			</div>
			<div class="clear">
				<button class="clear__completed">Clear Completed</button>
				<button class="clear__all">Clear All</button>
			</div>
			<div class="task">
				<input type="text" />
				<button></button>
			</div>
		</div>
	</div>

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

.container-wr {
	display: flex;
	align-items: center;
	justify-content: center;
	color: #aabbcc;
}

.container {
	max-width: 688px;
	padding: 16px;
}

.counter {
	display: flex;
	align-items: center;
	margin-bottom: 8px;
}

.counter p {
	font-family: "Nunito", sans-serif;
	font-size: 48px;
	font-weight: 400;
	font-style: normal;
	color: #0a0a0a;
	margin-right: 20px;
	line-height: 1.4;
}

.counter div {
	font-family: "Nunito", sans-serif;
	font-size: 48px;
	font-weight: 400;
	font-style: normal;
	color: #cacaca;
	line-height: 1.4;
	transform: translateY(-4px);
}
</style>
