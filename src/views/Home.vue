<template>
    <div>
        <h1>Hello World</h1>
        <Counter 
            :year="2024" 
            :month="3" 
            :date="23" 
            :hour="2" 
            :minute="33" 
            :second="34" 
            :millisecond="0" />
    </div>
</template>

<script setup>
import Counter from '@/components/Counter.vue'
</script>

<style lang="scss scoped">
</style>