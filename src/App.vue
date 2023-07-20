<script setup>
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <div>

  <div class="flex justify-center pt-16">
    <input type="text" 
          placeholder=" Write a movie name" 
          v-bind:value="inputText"
          v-on:input="inputChangeHandler"
    />
  </div>
  <div class = "flex justify-center pt-10">
    <button v-on:click="searchMovie" class="box-border h-11 w-40 border-4">Search</button>

  <div>
    <div class="bg-blue-400 w-32 h-64 m-4 p-8">
      {{ apiData }}
    </div>
    <div v-if="inputText != ''" class="bg-blue-400 w-32 h-64 m-4 p-8">
      {{ moviePlot }}
    </div>
  </div>
  </div>
      
  </div>
</template>

<script>
import axios from 'axios';
import { toHandlers } from 'vue';

export default {
  data() {
    return {
      apiData: [],
      inputText: '',
      moviePlot: '',
    }
  },
  methods: {
      inputChangeHandler(event) {
        this.inputText = event.target.value;
        axios
        .get(`https://www.omdbapi.com/?t=${this.inputText}&apikey=2b1b57fb`)
        .then(response => this.apiData = response.data.Title)
        .catch(error => {
            console.log(error);
        })
        if (this.inputText == ''){
          this.moviePlot = '';
        }

      },
      searchMovie() {
        axios
        .get(`https://www.omdbapi.com/?t=${this.inputText}&apikey=2b1b57fb`)
        .then(response => this.moviePlot = response.data.Plot)
        .catch(error => {
            console.log(error);
        })
        
      }

    }
   
} 
</script>

<style scoped>

</style>
