<template>
  <HeaderComponent title="Breaking Bad Api"/>
  <main class="container">
    <div class="select-category pt-5 pb-3 px-3">
      <select name="series-selector" id="series-selector">
        <option value="BB">Breaking Bad</option>
        <option value="BCS">Better Call Saul</option>
      </select>
    </div>
    <div class="charList p-5">
      <div v-if="loading">
        <div class="matches">
          Found {{characterList.length}} characters
        </div>
        <CharactersListComponent :characters="characterList" :load="loading"/>
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

  export default {
    components: { 
      HeaderComponent,
      CharactersListComponent
    },
    data(){
      return{
        apiURL: 'https://www.breakingbadapi.com/api/characters',
        characterList: [],
        loading: false
      }
    },
    methods: {
      callBBapi(){
        this.loading = false;
        axios.get(this.apiURL).then((res)=>{
          console.log(res.data);
          this.characterList = [...res.data];
          console.log(this.characterList);
          setTimeout(() => this.loading = true, 2000)
        })
      }
    },
    mounted(){
      this.callBBapi();
    }
}
</script>

<style lang="scss" scoped>
@use './assets/styles/partials/variables' as *;

  main{

    .select-category{
      
      #series-selector{
        padding: 10px;
        border-radius: 10px;
      }
    }

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
