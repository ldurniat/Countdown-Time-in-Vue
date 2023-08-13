<template>
    <div>
        <section class="text-3xl flex justify-center content-center flex-col mx-auto text-center"></section>
        <section class="flex text-6xl justify-center content-center">
            <div class="days mr-2 realtive">
                {{ displayDays }}
                <div class="label text-sm bottom-0">days</div>
            </div>
            <span class="leading-none">: </span>
            <div class="hours mx-2 realtive">
                {{ displayHours }}
                <div class="label text-sm bottom-0">hours</div>
            </div>
            <span class="leading-none">:</span>
            <div class="minutes mx-2 realtive">
                {{ displayMinutes }}
                <div class="label text-sm bottom-0">minutes</div>
            </div>
            <span class="leading-none">:</span>
            <div class="seconds ml-2 realtive">
                {{ displaySeconds }}
                <div class="label text-sm bottom-0">seconds</div>
            </div>
        </section>
    </div>
</template>

<script setup>
let displayDays    = 0
let displayHours   = 0
let displayMinutes = 0
let displaySeconds = 0
</script>

<style scoped>
.seconds {
    max-width: 60px;
}
</style>