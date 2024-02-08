<template>
    <div 
    class="indicator" 
    :class="{isActive}" 
    :style="{left: `${modelValue}%`}"
    @mousedown="e => handleMouseDown(e)">
    </div>
</template>

<script setup>
import {ref} from "vue"

const props = defineProps(["modelValue", "min", "max"])
const emit = defineEmits(["update:modelValue"])

const isActive = ref(false)

const handleMouseDown = (e) => {
    const scale = e.target.parentElement
    const scaleLeft = scale.getBoundingClientRect().left
    const scaleWidth = scale.getBoundingClientRect().width
    isActive.value = true
    const handleMouseMove = e => {
        const newValue = Math.round((e.clientX - scaleLeft) * 100 / scaleWidth)
        if (newValue > props.max || newValue < props.min) {
            return
        }
        emit("update:modelValue", newValue)
    }
    window.addEventListener("mousemove", handleMouseMove)
    window.addEventListener("mouseup", () => {
        isActive.value = false
        window.removeEventListener("mousemove", handleMouseMove)
    })
}
</script>

<style scoped>
.indicator {
    width: 20px;
    height: 20px;
    border-radius: 50%;
    background-color: white;
    border: 1px solid lightgray;
    position: absolute;
    z-index: 3;
    top: 50%;
    transform: translate(-50%, -50%);
}
.indicator:hover {
    cursor: pointer;
}
.isActive {
    box-shadow: 0 0 10px teal;
}
</style>