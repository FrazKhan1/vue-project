<script>
import { ref } from "vue";
export default {
  setup() {
    const name = ref("Fraz");
    const isActive = ref(true);
    const tasks = ref([1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]);
    const link = "https://example.com";

    const toggleActive = () => {
      isActive.value = !isActive.value;
    };

    return {
      name,
      isActive,
      tasks,
      toggleActive,
      link,
    };
  },
};
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="isActive">{{ name }} is active</p>
  <p v-else="isActive">{{ name }} is not active</p>

  <h3>
    <ul>
      <li v-for="t in tasks" :key="t">
        <a :href="link">
          {{ t }}
        </a>
      </li>
    </ul>
  </h3>

  <button @click="toggleActive">Change Status</button>
</template>
