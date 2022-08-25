<template>
  <base-card>
  <form @submit.prevent="submitData()">
    <div class="form-control">
      <label for="title">Title</label>
      <input id="title" name="title" type="text" v-model="title" />
    </div>
    <div class="form-control">
      <label for="desc">Description</label>
      <textarea id="desc" name="desc" rows="3" v-model="desc"></textarea>
    </div>
    <div class="form-control">
      <label for="link">Link</label>
      <input type="url" id="link" name="link" v-model="link" />
    </div>
    <div>
      <base-button type="submit" @click="submitData()">Add resources</base-button>
    </div>
    <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError()">
      <template #default>
        <p>Input is invalid!</p>
        <p>Please check it again!</p>
      </template>
      <template #actions>
        <base-button @click="confirmError()">Okay</base-button>
      </template>
    </base-dialog>
  </form>
  </base-card>
</template>

<script>
export default {
  inject: ['addResource'],

  data() {
    return {
      title: '',
      desc: '',
      link: '',
      inputIsInvalid: false
    };
  },

  methods: {
    submitData() {
      let title = this.title;
      let desc = this.desc;
      let link = this.link;

      if (title.trim() == '' || desc.trim() == '' || link.trim() == '') {
        return this.inputIsInvalid = true;
      }

      this.title = '';
      this.desc = '';
      this.link = '';
      this.addResource(title, desc, link);
    },

    confirmError() {
      this.inputIsInvalid = false;
    }
  }
}
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
