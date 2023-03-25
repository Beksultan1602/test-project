<template>
    <div class="stopwatch-container">
        <stopwatch v-for="item in stopwatches" />
        <div @click="addStopwatch" class="stopwatch-add">
            +
        </div>
    </div>
</template>

<script>

import Stopwatch from "@/components/Stopwatch";

export default {
    name: 'App',
    components: {
        Stopwatch,
    },
    data() {
        return {
            stopwatches: [1]
        }
    },
    methods: {
        addStopwatch() {
            this.stopwatches.push(1)
        }
    }
}
</script>

<style>
* {
    background: #353638;
}

.stopwatch-container {
    max-width: 1024px;
    width: 100%;
    margin: 0 auto;
    display: grid;
    grid-template-columns: auto auto auto;
    gap: 50px;
}

.stopwatch-add {
    background: #696969;
    height: 130px;
    width: 225px;
    color: #9E9E9E;
    display: flex;
    justify-content: center;
    align-items: center;
    font-weight: bold;
    cursor: pointer;
    margin: 0 auto;
}

@media screen and (max-width: 768px) {
    .stopwatch-container {
        grid-template-columns: auto auto;
    }
}

@media screen and (max-width: 320px) {
    .stopwatch-container {
        grid-template-columns: auto;
    }
}
</style>
