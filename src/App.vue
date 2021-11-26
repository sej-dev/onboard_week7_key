<template>
  <button @click="reorder">순서 재배치</button>
  <ul>
    <li v-for="item in data" :key="item.key">
      {{ item.content }}
    </li>
  </ul>
</template>

<script>

import { ref, watchEffect } from 'vue';

export default {
  name: 'App',
  setup(){
    const data = ref([]);
    
    for(let i=0; i<5000; i++){
      data.value.push({
        key: `key-${i}`,
        content: `item-${i}`,
      });
    }

    const reorder = () => {
      
      for(let i=0; i<data.value.length; i++){
        
        const idx1 = Math.floor( Math.random() * data.value.length );
        const idx2 = Math.floor( Math.random() * data.value.length );
        
        const item2 = data.value[idx2];
        data.value[idx2] = data.value[idx1];
        data.value[idx1] = item2;
      }
    };
    
    return {
      data,
      key: 0,
      reorder
    }
  }
}
</script>

<style>

  ul{
    display: flex;
    flex-wrap: wrap;
  }
  li {
    width: 100px;
  }

</style>
