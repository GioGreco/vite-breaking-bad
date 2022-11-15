<template>
  <HeaderComponent title="Breaking Bad Api"/>
  <main class="container">
    <FilterComponent @filtCat="callBBapi"/>
    <div class="charList p-5">
      <div v-if="store.loading">
        <div class="matches">
          Found {{store.characterList.length}} characters
        </div>
        <CharactersListComponent/>
      </div>
      <div v-else class="loading d-flex justify-content-center align-items-center">
        <div class="position-relative w-100 h-100">
          <div class="position-absolute grey circle"></div>
          <div class="position-absolute darkgrey circle"></div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import axios from 'axios';
import HeaderComponent from './components/HeaderComponent.vue';
import CharactersListComponent from './components/CharactersListComponent.vue'

import {store} from './store';
import FilterComponent from './components/FilterComponent.vue';

  export default {
    components: {
    HeaderComponent,
    CharactersListComponent,
    FilterComponent,
},
    data(){
      return{
        store,
        endpoint: 'characters'
      }
    },
    methods: {
      callBBapi(){
        store.loading = false;

        const currentEndpoint = store.apiURL + this.endpoint;

        let myFilter = {
          params: {
            category: store.categorySelector
          }
        }

        axios.get(currentEndpoint, myFilter).then((res)=>{
          store.characterList = [...res.data];
          setTimeout(() => store.loading = true, 2000)
        })
      }
    },
    created(){
      this.callBBapi();
    }
}
</script>

<style lang="scss" scoped>
@use './assets/styles/partials/variables' as *;

  main{
    .charList{
      background-color: white;

      .matches{
        background-color: $black-bar;
        color: white;
        padding: 15px;
      }

      .circle{
        height: 40px;
        width: 40px;
        border-radius: 50%;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        animation: loading 1s infinite;

        &.grey{
          background-color: $grey-card-frame;
        }
        &.darkgrey{
          background-color: $grey-text;
          animation: loading 1s infinite .5s;
        }
      }

      @keyframes loading {

        0%{
          transform: translate(-50%,-50%) scale(.2);
        }
        50%{
          transform: translate(-50%, -50%) scale(1);
        }
        100%{
          transform: translate(-50%,-50%) scale(.2);
        }
        
      }
    }
  }

</style>
