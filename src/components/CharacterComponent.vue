<template>
    <div class="col-12 col-sm-6 col-md-4 col-lg-3">
        <div class="char-card pb-5">
            <div class="char-pic">
                <img :src="character.img" :alt="character.name">
            </div>
            <div class="char-info">
                <h5 class="py-3 text-uppercase">{{character.name}}</h5>
                <p class="m-0 pb-1">{{character.category}}</p>
                <span>{{character.status}}</span>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'CharacterComponent',
        props: {
            character: Object
        }
    }
</script>

<style lang="scss" scoped>
@use '../assets/styles/partials/variables' as *;
    .char-card{
        background-color: $grey-card-frame;
        height: 500px;
        .char-pic{
            padding: 15px;
            height: 320px;

            img{
                width: 100%;
                height: 100%;
                object-fit: cover;
                object-position: top;
            }
        }
        .char-info{
            text-align: center;
            color: $grey-text;

            h5{
                color: white;
                font-weight: 700;
            }
            p{
                font-size: 1.2rem;
            }
        }
    }
</style>