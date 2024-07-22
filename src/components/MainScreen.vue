<template>
    <div class="sreen">
        <h1>POKE MEMORIES</h1>
        <p>Select mode to start game</p>
        <div class="action">
            <button @click="onStart(16)">
                <span>4x4</span>
                <span>Easy</span>
            </button>
            <button @click="onStart(36)">
                <span>6x6</span>
                <span>Nomal</span>
            </button>
            <button @click="onStart(64)">
                <span>8x8</span>
                <span>Hard</span>
            </button>
            <button @click="onStart(100)">
                <span>10x10</span>
                <span>Master</span>
            </button>
        </div>
    </div>
</template>

<script>
    export default {
        methods: {
            onStart(totlalOfBlocks) {
                this.$emit("onStart", {totlalOfBlocks})
            }
        }
    }
</script>