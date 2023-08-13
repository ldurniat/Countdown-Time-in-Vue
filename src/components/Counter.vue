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
import { computed, onMounted } from 'vue'

let displayDays    = 0
let displayHours   = 0
let displayMinutes = 0
let displaySeconds = 0

const _seconds = computed( () => { return 1000 } )
const _minutes = computed( () => { return _seconds * 60 } )
const _hours   = computed( () => { return _minutes * 60 } )
const _days    = computed( () => { return _hours * 24 } )

function showRemaining() {
    const timer = setInterval( () => {
        const now = new Date(2023, 4, 22, 10, 7, 8, 9)
        const end = new Date(2023, 4, 22, 10, 10, 10, 10)
        const distance = end.getTime() - now.getTime()

        if(distance < 0) {
            clearInterval(timer)
            return
        }

        const days     = Math.floor(distance / _days)
        const hours    = Math.floor((distance % _days) / _hours)
        const minutes  = Math.floor((distance % _hours) / _minutes)
        const seconds  = Math.floor((distance % _minutes) / _seconds)
        displaySeconds = seconds < 10 ? '0' + seconds : seconds
        displayMinutes = minutes < 10 ? '0' + minutes : minutes
        displayHours   = hours < 10 ? '0' + hours : hours
        displayDays    = days < 10 ? '0' + days : days  
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