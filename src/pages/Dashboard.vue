<script setup>
import Card from "../components/Card.vue";
import { ref, onMounted } from "vue";

const users = ref([]);

onMounted(async () => {
  try {
    const response = await fetch(
      "https://api.slingacademy.com/v1/sample-data/users"
    );
    const data = await response.json();
    users.value = data;

    // Menampilkan data JSON ke konsol
    console.log(data);
  } catch (error) {
    console.error("Error fetching data:", error);
  }
});
</script>

<template>
  <div class="flex gap-5 flex-wrap mb-10">
    <Card />
    <Card />
    <Card />
  </div>
  <div class="bg-white rounded-lg shadow">
    <h2 class="text-zinc-950 font-semibold p-6">Users List</h2>
    <table class="w-full">
      <thead>
        <tr class="bg-gray-50">
          <th class="p-3">ID</th>
          <th>Users</th>
          <th>Date Of Birth</th>
          <th>Email</th>
          <th>Job</th>
          <th>Country</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in users" :key="user.id">
          <td>{{ user.id }}</td>
          <td>{{ user.name }}</td>
          <td>{{ user.date_Of_Birth }}</td>
          <td>{{ user.email }}</td>
          <td>{{ user.job }}</td>
          <td>{{ user.country }}</td>
          <td>
            <button class="p-5 bg-white rounded shadow">View Detail</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
