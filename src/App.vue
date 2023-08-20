<script setup>
import { ref } from 'vue'
import TreeItem from './TreeItem.vue'

const treeData = ref({
  name: 'Root node',
  children: [
    { name: 'Child 1', data:'c1 data1' },
    { name: 'Child 2', data:'c2 data2' },
    {
      name: 'Child folder',
      children: [
        {
          name: 'Child folder',
          children: [{ name: 'Child', data:'data' }, { name: 'Child', data: 'data' }]
        },
      ]
    }
  ]
})


const displayObject =ref(false);
</script>

<template>
  <div >
    <div>
      <TreeItem class="item" :model="treeData"></TreeItem>
    </div>
    <div class="button-container">

      <button class="export-button" @click="()=>{displayObject=true}">Export</button>
    </div>
    <div v-show="displayObject" style="margin:4rem; height: max-content; width: max-content; background-color: aliceblue; border-radius: 23px;">
      <p v-show="displayObject" style="margin: 0; font-size: 3rem; padding: 2rem;">Tree Data</p>
      <pre style="; padding: 2rem;" >{{ displayObject? JSON.stringify(treeData,null,2):null }}</pre>
    </div>
  </div>
</template>

<style>
body {
  padding: 4rem;
  background-color:#0F0016;
}
  .box {
  
    border: 3px solid;
    border-radius: 23px;
    margin: 5px;
    margin-left: 20px;
  }
.item {
  background-color:#302532;
  border: 1px solid rgba(255, 255, 255, 0.14);
  cursor: pointer;
  line-height: 1.5;
}

.button-container {
  height:2rem;
  width: 10rem;
}

.export-button {
  margin: 2rem;
  height: 100%;
  width: 80%;
}

.bold {
  font-weight: bold;
}
</style>