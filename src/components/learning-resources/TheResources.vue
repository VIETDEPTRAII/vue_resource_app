<template>
  <base-card>
    <base-button class="mr-2" @click="selectTab('stored-resources')" :mode="storedResButtonMode">Stored Resources</base-button>
    <base-button @click="selectTab('add-resource')" :mode="addResButtonMode">Add Resource</base-button>
  </base-card>
  <keep-alive>
    <component :is="currentTab"></component>
  </keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default {
  components: {
    StoredResources,
    AddResource
  },

  data() {
    return {
      currentTab: 'stored-resources',
      storedResources: [
        {
          id: 1,
          title: 'Resource 1',
          desc: 'Description of the resource 1',
          link: 'https://vuejs.org/'
        },
        {
          id: 2,
          title: 'Resource 2',
          desc: 'Description of the resource 2',
          link: 'https://vuejs.org/'
        }
      ]
    };
  },

  provide() {
    return {
      storedResources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.deleteResource
    };
  },

  methods: {
    selectTab(tab) {
      this.currentTab = tab;
    },

    addResource(title, desc, link) {
      const resource = {
        id: new Date().toISOString(),
        title: title,
        desc: desc,
        link: link
      }
      this.storedResources.unshift(resource);
      this.currentTab = 'stored-resources';
    },

    deleteResource(resId) {
      const resIndex = this.storedResources.findIndex(res => res.id == resId);
      this.storedResources.splice(resIndex, 1);
    }
  },

  computed: {
    storedResButtonMode() {
      return this.currentTab == 'stored-resources' ? null : 'flat';
    },

    addResButtonMode() {
      return this.currentTab == 'add-resource' ? null : 'flat';
    }
  }
}
</script>
