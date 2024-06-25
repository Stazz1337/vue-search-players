<template>
  <div class="search-component">
    <input type="text" v-model="searchQuery" placeholder="Введите имя игрока" />
    <ul v-if="filteredPlayers.length > 0 && searchQuery.length >= 3" class="autocomplete-list">
      <li v-for="(player, index) in filteredPlayers.slice(0, 10)" :key="index" @click="selectPlayer(player)">
        {{ player.name }}
      </li>
    </ul>
    <table v-if="selectedPlayer" class="profile-table">
      <thead>
        <tr>
          <th>Имя</th>
          <th>Возраст</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>{{ selectedPlayer.name }}</td>
          <td>{{ selectedPlayer.age }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const players = [
  { name: 'Игрок 1', age: 20},
  { name: 'Игрок 2', age: 22 },
  { name: 'Игрок 3', age: 22 },
  { name: 'Игрок 4', age: 22 },
  { name: 'Игрок 5', age: 22 },
  { name: 'Игрок 6', age: 22 },
  { name: 'Игрок 7', age: 22 },
  { name: 'Игрок 8', age: 22 },
  { name: 'Игрок 9', age: 22 },
  { name: 'Игрок 10', age: 22 },
  { name: 'Игрок 11', age: 22 },
];

let searchQuery = ref('');
let selectedPlayer = ref(null);

const filteredPlayers = computed(() => {
  return players.filter(player => player.name.toLowerCase().includes(searchQuery.value.toLowerCase()));
});

function selectPlayer(player) {
  selectedPlayer.value = player;
}
</script>

<style scoped>
.search-component {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.autocomplete-list {
  list-style-type: none;
  padding: 0;
  margin-top: 5px;
}

.profile-table {
  margin-top: 20px;
}
</style>