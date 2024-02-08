<template>
    <div class="scale">
        <Indicator v-model="minNum" :min="0" :max="maxNum"/>
        <Indicator v-model="maxNum" :min="minNum" :max="100"/>
        <div class="range" :style="{left: `${minNum}%`, right: `${100 - maxNum}%`}"></div>
    </div>
    <div class="values">
        <label for="min">Min</label>
        <InputNumber v-model.number="minNum" :min="0" :max="maxNum" id="min"/>
        <label for="max">Max</label>
        <InputNumber v-model.number="maxNum" :min="minNum" :max="100" id="max"/>
    </div>
</template>

<script setup>
import {ref} from "vue"
import InputNumber from './InputNumber.vue'
import Indicator from "./Indicator.vue"

const minNum = ref(5)
const maxNum = ref(30)
</script>

<style scoped>
.scale {
    height: 2px;
    width: 400px;
    background-color: lightgray;
    position: relative;
}
.range {
    position: absolute;
    height: 100%;
    background-color: teal;
}
.values {
    display: flex;
    align-items: center;
    gap: 10px;
    user-select: none;
}
</style>