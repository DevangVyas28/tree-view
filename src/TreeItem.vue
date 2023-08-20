<!-- eslint-disable vue/no-mutating-props -->
<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
  model: Object
})

const setTitle=ref(true)
const isOpen = ref(false)
const isFolder = computed(() => {
  return props.model.children && props.model.children.length
})

function toggle() {
  isOpen.value = !isOpen.value
}

function changeType() {
  if (!isFolder.value) {
    props.model.children = []
    addChild()
    isOpen.value = true
  } else {
    addChild()
  }
}

function addChild() {
  props.model.children.push({ name: 'New Child', data:'New Data' })
}



</script>

<template>
  <div class="box">
    <div class="title-bar">
      <div class="title-container">
        <div  @click="toggle" style="margin:0 1rem; height: 1rem; width: 3rem; display: flex; align-items: center; justify-content: center; ">
          <span >{{ isOpen ? 'v' : '>' }}</span>
        </div>
        <div
        v-if="setTitle"
        :class="{ bold: isFolder , inside}"
        style="margin-right: 20px;" 
        @click="setTitle=!setTitle">
        {{model.name}}      
      </div>
      <input v-else :value="model.name" v-on:keydown.enter="(event)=>{ model.name=event.target.value; setTitle= !setTitle}" />
    </div>
    <div class="add-button" @click="changeType"> 
      Add child
    </div>
    </div>
    <div class="data-field" v-show="!isFolder && isOpen" style="margin-left: 4rem; padding:1rem;">Data<textarea  :value=model.data @input="event=>model.data = event.target.value"  style="border-radius: 10px; padding-left:0.5rem; padding-top: 0.3rem;"></textarea></div>
    <div v-show="isOpen" v-if="isFolder">
      
      <TreeItem
        class="item"
        v-for="model in model.children"
        :model="model">
      </TreeItem>
      
    </div>
  
</div>
</template>

<style>


.title-bar {
    
    padding:8px;
    border-radius:23px 23px 0 0;
    display: flex;
    align-items: center;
    justify-content: space-between;
    background-color: #CBC8CC;
}

.title-container {
  display: flex;
  align-items: center;
}

.add-button {
  margin-right: 1rem;
  width:8%;
  text-align: center;
  background-color: white;
  border-radius: 23px;
}

.data-field {
    margin: 0.5rem;
    height: 2rem;
    width: 15rem;
    display: flex;
    text-align: center;
    border: 2px solid;
    border-radius: 10px;
    justify-content: space-between;
    background-color: #CBC8CC;
}



</style>