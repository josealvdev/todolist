<script setup>
defineProps({
    name: String
})
</script>

<template>
    <div class="row align-items-center tarea">
        <input class="col-1 form-check-input" @click="$emit('changeCheck')" type="checkbox" id="check"> 
        <label for="check" class="col-10">{{name}}</label>
        <button class="col-1" @click="$emit('delete')"><i class="bi bi-trash-fill"></i></button>
    </div>
</template>

<style scoped>
 .tarea{
    margin: 0px;
    padding: 10px 0px 10px 0px;

    input[type="checkbox"] {
        height: 25px;
        width: 15px;
        border-radius: 50%;
    }

    label {
        font-weight: 600;
        font-size: 16px;
    }

    button {
        padding: 0px !important;
        background: none;
        border: 0;
        width: 10%;
        text-align: right;
    }

    i {
        font-size: 23px;
    }
 }
</style>