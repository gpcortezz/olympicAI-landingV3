<template>
  <div class="box"></div>
</template>

<script setup>
import { onMounted } from "vue";
import { gsap } from "gsap";

onMounted(() => {
    gsap.to(".box", { 
        x: 200,
    });
});
</script>

<style scoped>
template {
    display: flex;
    align-items: center;
    justify-content: flex-start;
    min-height: 100vh;
    margin: 0;
    overflow: hidden;
}

.box {
    display: block;
    width: 100px;
    height: 100px;
    background-color: green;
}
</style>