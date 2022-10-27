
<script setup>

  import {ref, computed} from 'vue'

  const counter = ref(0)
  const arrayFav = ref([])

  const name = 'Vue dinamico'

  const increment = () => {
    counter.value++;
  }

  const decrement = () => {
    counter.value--;
  }

  const reset = () => {
    counter.value=0
  }

  const add = ()=> {
    arrayFav.value.push(counter.value)
  }


  const blockBtnAdd = computed(() => {

    const numSearch = arrayFav.value.find(num => num === counter.value);
    console.log(numSearch);

    // 2 maneras:

    //1.-
    //Cuando es 0
    // if(numSearch === 0) return true
    // return numSearch ? true : false;


    // 2.-
    return numSearch || numSearch === 0


  })


  const classCounter = computed(() => {
    if(counter.value === 0){
      return 'zero'
    }

    if(counter.value > 0){
      return 'positive'
    }

    if(counter.value < 0){
      return 'negative'
    }

  })


</script>


<template>

  <div class="container text-center mt-3">

    <h1>Hola {{ name.toUpperCase()}}</h1>
    
    <h2 :class="classCounter">{{ counter }}</h2>


    <div class="btn-group">

      <button @click="increment" class="btn btn-success">Aumentar</button>

      <button @click="decrement" class="btn btn-danger">Disminuir</button>

      <button @click="reset" class="btn btn-secondary">Reset</button>

      <button @click="add" :disabled="blockBtnAdd" class="btn btn-primary">Add</button>

    </div>


    <ul class="list-group">
      <li 
        v-for="(num, index) in arrayFav"
        :key="index"
        class="list-group-item"
      >
        {{ num }}
      </li>
    </ul>


  </div>


  

</template>


<style>

.positive{
  color: green;
}

.negative{
  color: red;
}

.zero{
  color: peru;
}

</style>