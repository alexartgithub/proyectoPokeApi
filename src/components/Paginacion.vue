<script setup>
defineProps(['inicio','final','maxLength']);
const emit = defineEmits(['siguiente','anterior']);
const activarSiguiente = () =>{
    console.log("me diste a siguiente");
    emit("siguiente");
}
</script>
<template>
    <div class="d-flex flex-row justify-content-around mt-2 mb-2">
        <button class="btn btn-primary" type="button" @click="emit('anterior')" :disabled="inicio<=0"> Atras</button>
        <span>{{ inicio }}/{{ final }} de {{ maxLength }}</span>
        <button class="btn btn-primary" type="button" @click="activarSiguiente" :disabled="final>=maxLength"> Siguiente</button>
    </div>
</template>