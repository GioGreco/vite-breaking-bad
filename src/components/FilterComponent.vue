<template>
    <div class="select-category pt-5 pb-3 px-3">
      <form @submit.prevent="filterPerCategory" class="d-flex align-items-center">
        <select v-model="store.categorySelector" name="series-selector" id="series-selector">
          <option selected value="">Select category...</option>
          <option value="Breaking Bad">Breaking Bad</option>
          <option value="Better Call Saul">Better Call Saul</option>
        </select>
        <button type="submit" class="btn btn-primary text-uppercase mx-3">Filtra per serie</button>
        <button @click="resetFilter" type="reset" class="btn btn-danger"><i class="fa-solid fa-ban"></i></button>
      </form>
    </div>
</template>

<script>
import {store} from '../store';

    export default {
        name: 'FilterComponent',
        data(){
            return{
                store
            }
        },
        // watch: {
        //     store: {
        //         handler: 'this.$parent.callBBapi()'
        //     }
        // },
        methods: {
            filterPerCategory(){
                this.$emit('filtCat');
                console.log(store);
            },
            resetFilter(){
                store.categorySelector = '';
                this.$emit('filtCat')
            }
        }
    }
</script>

<style lang="scss" scoped>
    #series-selector{
        color: black;
        padding: 10px;
        border-radius: 10px;
    }
</style>