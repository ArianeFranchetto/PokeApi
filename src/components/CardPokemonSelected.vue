<script setup>
const pokemon = defineProps(["name", "xp", "id", "weight", "img"])

</script>

<template>
    <div id="card-pokemon" class="card">
        <img :src="pokemon.img" class="card-img-top" alt="...">
        <div class="card-body">
            <h5 class="card-title text-center">{{ pokemon.name }}</h5>
            <hr>
            <div class="row">
                <section class="col">
                    <strong>XP:</strong>
                    <span>{{ pokemon.xp }}</span>


                </section>
                <section class="col">

                    <strong>Number:</strong>
                    <span v-show="pokemon.id"> {{ pokemon.id }}</span>

                </section>

                <section class="col">

                    <strong>Weight:</strong>
                    <span v-show="pokemon.weight"> {{ pokemon.weight }}</span>

                </section>
            </div>

        </div>
    </div>
</template>

<style>
#card-pokemon {
    display: flex;
    align-items: center;
    width: 500px;
    background: rgb(131, 58, 180);
    background: linear-gradient(90deg, rgba(131, 58, 180, 1) 0%, rgba(253, 29, 29, 1) 50%, rgba(252, 176, 69, 1) 100%);

}

.card-img-top{
    width: 200px;

}
</style>