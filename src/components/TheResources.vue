<template>
  <base-card>
    <base-button
      @click="setSelectedTab('stored-resource')"
      :mode="storedResButtonsMode"
      >Show Items</base-button
    >
    <base-button
      @click="setSelectedTab('add-resource')"
      :mode="addResButtonMode"
    >
      Add New Item</base-button
    >
  </base-card>
  <keep-alive>
    <component :is="selectedTab" @add-item="addItem"></component>
  </keep-alive>
</template>

<script>
import BaseButton from '../UI/ BaseButton.vue';
import BaseCard from '../UI/BaseCard.vue';
import StoredResource from './StoredResource.vue';
import AddResource from './AddResource.vue';
export default {
  components: { BaseCard, BaseButton, StoredResource, AddResource },
  data() {
    return {
      selectedTab: 'stored-resource',
      resourcesData: [
        {
          id: 'official-guide',
          title: 'Official guide',
          desc: 'the official vue.js documentation',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'Google',
          desc: 'google helops developers alot',
          link: 'https://google.com',
        },
      ],
    };
  },
  provide() {
    return {
      storedResources: this.resourcesData,
      deleteItem: this.deleteItem,
    };
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addItem(item) {
      this.resourcesData.push(item);
      this.selectedTab = 'stored-resource';
    },
    deleteItem(id) {
      const index = this.resourcesData.findIndex((item) => item.id === id);
      this.resourcesData.splice(index, 1);
    },
  },
  computed: {
    storedResButtonsMode() {
      return this.selectedTab === 'stored-resource' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    },
  },
};
</script>

<style></style>
