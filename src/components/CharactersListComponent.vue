<template>
    <div class="row p-3 g-4">
        <CharacterComponent v-for="(item, index) in characters" :key="item.char_id" :character="item"/>
    </div>
</template>

<script>
import CharacterComponent from './CharacterComponent.vue';

    export default {
        name: 'CharactersListComponent',
        components: {
            CharacterComponent
        },
        props: {
            characters: Object,
            load: Boolean
        }
    }
</script>

<style lang="scss" scoped>

</style>