<template>
    <input 
    type="number" 
    @input="handleInput" 
    :value="modelValue">
</template>

<script setup>
defineProps(["modelValue"])
const emit = defineEmits(["update:modelValue"])

const handleInput = (e) => {
    if (+e.target.value > +e.target.max || +e.target.value < +e.target.min) {
        return
    }
    emit("update:modelValue", e.target.value)
}
</script>

<style scoped>
input {
    border: 1px solid lightgray;
    border-radius: 5px;
    padding: 5px;
}
</style>