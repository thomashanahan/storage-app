<template>
  <div class="main-image">
    <h2>{{valueOfImage.title}}</h2>
    <div>
      <div class="col-sm-3">
        <span class="image">
          <img :src="valueOfImage.url" :width="450" alt>
        </span>
      </div>
      <div class="col-sm-9">
        <p>{{valueOfImage.description}}</p>
      </div>
      <button @click="download(valueOfImage.url)">
        Download!
      </button>
    </div>
  </div>
</template>
<script>
import { ipcRenderer } from "electron";
export default {
  async fetch({ store , params, route}) {
    console.log(route.params.id);
    await store.dispatch("GET_VALUE_OF_IMAGE", route.params.id);
  },
  computed: {
    valueOfImage() {
      return this.$store.getters.valueOfImage
        ? this.$store.getters.valueOfImage
        : [];
    }
  },
  methods: {
    download(url){
      console.log(url);
      ipcRenderer.send('download', {
          url: url});
    }
  }
}
</script>
<style scoped>
.main-image{
  padding: 30px;
}
</style>