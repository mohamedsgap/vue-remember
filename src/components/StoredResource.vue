<template>
  <ul>
    <list-item
      v-for="resource in storedResources"
      :key="resource.id"
      :resource="resource"
      @delete-resource="deleteResource"
    ></list-item>
  </ul>
</template>

<script>
import ListItem from './ListItem.vue';
export default {
  components: {
    ListItem,
  },
  inject: ['storedResources'],
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>
