<template>
  <base-dialog title="Invalid Data" v-if="showError" @close="handleDialog">
    <template #default>
      <p>there is an imput value is invalid</p>
    </template>
    <template #actions>
      <base-button @click="handleDialog">Okay</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form>
      <div class="form-control">
        <label for="title">Title</label>
        <input type="text" id="title" name="title" v-model="title" />
      </div>
      <div class="form-control">
        <label for="Description">Description</label>
        <textarea row="3" id="Description" name="Description" v-model="desc" />
      </div>
      <div class="form-control">
        <label for="Link">Link</label>
        <input type="url" id="Link" name="Link" v-model="link" />
      </div>
      <div>
        <base-button type="submit" @click="addItem"> Add Resource </base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
import BaseButton from '../UI/ BaseButton.vue';
import BaseCard from '../UI/BaseCard.vue';
import BaseDialog from '../UI/BaseDialog.vue';
export default {
  components: { BaseCard, BaseButton, BaseDialog },
  emits: ['add-item'],
  methods: {
    addItem(e) {
      e.preventDefault();
      if (
        this.title.trim() === '' ||
        this.desc.trim() === '' ||
        this.link.trim() === ''
      ) {
        //
        this.showError = true;
      } else {
        this.$emit('add-item', {
          id: Date.now(),
          title: this.title,
          desc: this.desc,
          link: this.link,
        });
      }
    },
    handleDialog() {
      this.showError = false;
    },
  },
  data() {
    return {
      title: '',
      link: '',
      desc: '',
      showError: false,
    };
  },
};
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
