<script setup>
import { computed, ref } from 'vue';

  const name = "Vue dinamico";

  const counter = ref(0);

  const increment = ()=>{
    counter.value++;
  };

  const arrayFavorites = ref([]);
  const decrement =() => counter.value--;
  const reset=()=>{
    counter.value=0;
  };

  const classCounter = computed(()=>{
    if(counter.value == 0){
      return 'zero'
    }
    if(counter.value > 0){
      return 'positive'
    }
    if(counter.value < 0){
      return 'negative'
    }
  });
  const add =()=>{
    arrayFavorites.value.push(counter.value);

  }

  const bloquearBtnAdd = computed (() => {
    const numSearch = arrayFavorites.value.find((num) => num == counter.value)
    console.log(numSearch);
    if (numSearch == 0) return true;
    return numSearch ? true : false;
    //return numSearch || numSearch == 0;
  });
  
</script>

<template>
  <div class="container text-center mt-3">
    <h1>Hola {{ name.toUpperCase() }}</h1>
    <h2 :class="classCounter">{{ counter }}</h2>
    <div class="btn-group">
      <button @click="increment" class="btn btn-success">Aumentar</button>
      <button @click="decrement" class="btn btn-danger">Disminuir</button>
      <button @click="reset" class="btn btn-secondary">Reset</button>
      <button @click="add" class="btn btn-primary" :disabled="bloquearBtnAdd">Add</button>
    </div>

    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="(num, index) in arrayFavorites" :key="index">
        {{ num }}
      </li>

    </ul>
  </div>
</template>

<style>
  h1{
    color: red;
  }
  .positive{
    color: green;
  }
  .negative{
    color: red;
  }
  .zero{
    color: blue;
  }
</style>