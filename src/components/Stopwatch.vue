<template>
    <div :style="playerStatus ? {'backgroundColor': '#777'} : ''" class="stopwatch">
        <div class="stopwatch-top">
            <p
                :style="playerStatus ? {'color': 'white'} : ''"
                v-if="hours !== 0"
                class="stopwatch-timer"
            >
                {{ hours }}:
            </p>
            <p
                :style="playerStatus ? {'color': 'white'} : ''"
                v-if="minutes !== 0 || hours > 0"
                class="stopwatch-timer"
            >
                {{ minutes }}:
            </p>
            <p
                :style="playerStatus ? {'color': 'white'} : ''"
                class="stopwatch-timer"
            >
                {{ currentTime }}
            </p>
        </div>
        <hr
            class="stopwatch-half"
            :style="playerStatus ? {'border': '1px #fff solid'} : ''"
        >
        <div class="stopwatch-items">
            <button v-if="!playerStatus" @click="startTimer">
                <img src="@/assets/start.png" alt="">
            </button>
            <button v-if="playerStatus" @click="stopTimer">
                <img src="@/assets/stop.png" alt="">
            </button>
            <button v-if="!playerStatus" @click="clearTimer">
                <img src="@/assets/clear.png" alt="">
            </button>
            <button v-if="playerStatus" @click="clearTimer">
                <img src="@/assets/white-clear.png" alt="">
            </button>
        </div>
    </div>
</template>

<script>
export default {
    name: "Stopwatch",
    data() {
        return {
            currentTime: 0,
            minutes: 0,
            hours: 0,
            interval: null,
            playerStatus: false
        }
    },
    methods: {
        startTimer() {
            this.interval = setInterval(this.timeIncrease, 1000)
            this.playerStatus = true
        },
        stopTimer() {
            clearInterval(this.interval)
            this.interval = null
            this.playerStatus = false
        },
        timeIncrease() {
            this.currentTime++
        },
        clearTimer() {
            clearInterval(this.interval)
            this.currentTime = 0
            this.playerStatus = false
        },
    },
    watch: {
        currentTime() {
            if(this.currentTime !== 0 && this.currentTime % 60 === 0) {
                this.currentTime = 0
                this.minutes++
            }
        },
        minutes() {
            if(this.minutes !== 0 && this.minutes % 60 === 0) {
                this.minutes = 0
                this.hours++
            }
        }
    }
}
</script>

<style scoped>
.stopwatch {
    max-width: 225px;
    width: 100%;
    background: #696969;
    position: relative;
    margin: 0 auto;
}
.stopwatch-top {
    background: transparent;
    padding: 22px 75px;
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
}
.stopwatch-timer {
    font-family: 'Gotham Pro';
    font-style: normal;
    font-weight: 400;
    font-size: 22px;
    line-height: 21px;
    color: #9E9E9E;
    background: transparent;
    margin: 0;
    text-align: center;
}
.stopwatch-half {
    position: absolute;
    left: 0;
    border: 1px #9E9E9E solid;
    margin: 0;
    max-width: 223px;
    width: 100%;
}
.stopwatch-items {
    background: transparent;
    display: flex;
    justify-content: space-evenly;
    padding: 20px 0;
}
.stopwatch-items button {
    background: transparent;
    border: none;
    cursor: pointer;
}
.stopwatch-items img {
    background: transparent;
}
</style>