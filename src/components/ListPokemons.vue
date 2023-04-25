
<script setup>
const pokemon = defineProps(["name", "urlBaseSvg"])

</script>

<template>
    <div id="main-card" class="col-4">
        <div id="card" class="card p-1 mb-3">
            <p class="text-center">{{ pokemon.name }}</p>
            <img :src="urlBaseSvg" class="card-img-top" alt="..." height="75">

        </div>
    </div>
</template>

<style scoped>
#main-card {
    align-items: center;
}

#card {
    background: rgb(34, 193, 195);
    background: linear-gradient(0deg, rgba(34, 193, 195, 1) 0%, rgba(253, 187, 45, 0.8940826330532213) 100%);
    cursor: pointer;

}

#card:hover {
    background: rgb(2, 0, 36);
    background: linear-gradient(90deg, rgba(2, 0, 36, 1) 0%, rgba(121, 9, 88, 1) 48%, rgba(49, 130, 188, 1) 77%, rgba(33, 156, 209, 1) 84%, rgba(0, 212, 255, 1) 100%);
    color: #fff;
}

#card:hover img:hover {
    padding: .2rem;
}
</style>