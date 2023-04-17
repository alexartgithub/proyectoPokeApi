<script setup>
defineProps({
    name :String,
    url : String,
});

const emits = defineEmits(['elegirFavorito']);

</script>

<template>
    <div class=" card mb-2">
        <div class="card-body d-flex flex-column">
            <h4 class="card-title text-center">{{ name.toUpperCase() }}</h4>
            <a :href="url" class=" d-inline text-center mb-2"> Página de {{ name.toUpperCase() }}</a>
            <button class="btn btn-primary" @click="emits('elegirFavorito',name)">Elegir</button>
        </div>
    </div>  
</template>