<template>
  <li>
    <base-card>
      <header>
        <h3>{{ resource.title }}</h3>
        <base-button mode="flat" @click="deleteResource(resource.id)"
          >Delete</base-button
        >
      </header>
      <p>{{ resource.desc }}</p>
      <nav>
        <a :href="resource.link">{{ resource.link }}</a>
      </nav>
    </base-card>
  </li>
</template>

<script>
import BaseButton from '../UI/ BaseButton.vue';
import BaseCard from '../UI/BaseCard.vue';
export default {
  components: { BaseCard, BaseButton },
  props: {
    resource: Object,
  },
  methods: {
    deleteResource(id) {
      this.$emit('delete-resource', id);
    },
    emits: {
      deleteResource: Function,
    },
  },
};
</script>

<style scoped>
li {
  margin: auto;
  max-width: 40rem;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h3 {
  font-size: 1.25rem;
  margin: 0.5rem 0;
}

p {
  margin: 0.5rem 0;
}

a {
  text-decoration: none;
  color: #ce5c00;
}

a:hover,
a:active {
  color: #c89300;
}
</style>
