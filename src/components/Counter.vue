<template>
    <div v-if="loaded">
        <section class="text-3xl flex justify-center content-center flex-col mx-auto text-center">
            <h5 v-if="!expired">Buy Now</h5>
            <h5 v-else>Timer is Done</h5>
        </section>
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

const props = defineProps({
    year        : {type:Number, default:2028},
    month       : {type:Number, default:0},
    date        : {type:Number, default:1},
    hour        : {type:Number, default:1},
    minute      : {type:Number, default:0},
    second      : {type:Number, default:0},
    millisecond : {type:Number, default:0}
})

let displayDays    = ref(0)
let displayHours   = ref(0)
let displayMinutes = ref(0)
let displaySeconds = ref(0)

const loaded  = ref(false)
const expired = ref(false) 

const _seconds = computed( () => { return 1000 } )
const _minutes = computed( () => { return _seconds.value * 60 } )
const _hours   = computed( () => { return _minutes.value * 60 } )
const _days    = computed( () => { return _hours.value * 24 } )
const end      = computed( () => { return new Date(
                                                    props.year, 
                                                    props.month, 
                                                    props.date, 
                                                    props.hour, 
                                                    props.minute, 
                                                    props.second, 
                                                    props.millisecond
                                                ) } )

function formatNum(num) {
    return num < 10 ? '0' + num : num
}

function showRemaining() {
    const timer = setInterval( () => {
        const now      = new Date()
        const distance = end.value.getTime() - now.getTime()

        if(distance < 0) {
            clearInterval(timer)
            expired.value = true
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
        
        loaded.value = true
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