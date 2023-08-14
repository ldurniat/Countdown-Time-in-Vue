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
import { computed, onMounted, ref } from 'vue'

let displayDays    = ref(0)
let displayHours   = ref(0)
let displayMinutes = ref(0)
let displaySeconds = ref(0)

const _seconds = computed( () => { return 1000 } )
const _minutes = computed( () => { return _seconds.value * 60 } )
const _hours   = computed( () => { return _minutes.value * 60 } )
const _days    = computed( () => { return _hours.value * 24 } )

function formatNum(num) {
    return num < 10 ? '0' + num : num
}

function showRemaining() {
    const start = new Date()
    const timer = setInterval( () => {
        const now = new Date()
        const end = new Date(start.getTime() + 2 * _hours.value)
        const distance = end.getTime() - now.getTime()

        if(distance < 0) {
            clearInterval(timer)
            return
        }

        const days     = Math.floor(distance / _days.value)
        const hours    = Math.floor((distance % _days.value) / _hours.value)
        const minutes  = Math.floor((distance % _hours.value) / _minutes.value)
        const seconds  = Math.floor((distance % _minutes.value) / _seconds.value)
        displaySeconds.value = formatNum(seconds)
        displayMinutes.value = formatNum(minutes)
        displayHours.value   = formatNum(hours)
        displayDays.value    = formatNum(days)  
        console.log(displaySeconds.value)
    }, 1000 )
}

onMounted( () => {
    showRemaining()
} )
</script>

<style scoped>
.seconds {
    max-width: 60px;
}
</style>