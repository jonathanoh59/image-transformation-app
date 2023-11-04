<template>
  <div id="app" ref="dropRef" class="drop-zone">
    Drop files here

    <!-- Displaying the list of dropped files -->
    <ul v-if="droppedFiles.length">
      <li v-for="file in droppedFiles" :key="file.name">{{ file.name }}</li>
    </ul>
  </div>
</template>

<script>
import { ref } from 'vue';
import { useDropZone } from '@vueuse/core';

export default {
  name: 'App',
  setup() {
    const dropRef = ref(null);
    const droppedFiles = ref([]);  // Create a new ref to store the files

    useDropZone(dropRef, {
      onDrop: (files) => {
        console.log('Dropped files:', files);
        droppedFiles.value = [...files, ...droppedFiles.value];  // Update the droppedFiles ref with the new files
      },
    });

    return { dropRef, droppedFiles };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  border: 2px dashed #ccc;
  padding: 20px;
}
</style>
