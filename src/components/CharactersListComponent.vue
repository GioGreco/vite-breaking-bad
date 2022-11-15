<template>
    <div class="row p-3 g-4">
        <CharacterComponent v-for="(item, index) in store.characterList" :key="item.char_id" :character="item"/>
    </div>
</template>

<script>
import CharacterComponent from './CharacterComponent.vue';
import {store} from '../store';

    export default {
        name: 'CharactersListComponent',
        components: {
            CharacterComponent
        },
        data(){
            return{
                store,
            }
        }
    }
</script>

<style lang="scss" scoped>

</style>