<template>
    <ul>
        <div class="BONG">
            <img src="../assets/gong.jpg" @click.prevent="playSound('../assets/gong.m4a')"  @click="cookies++" >
        </div>
    </ul>
</template>
<script>
    new Vue(Sound,{
    el: '#BONG',
    data: {
        text: 'BONG'
    },
    methods: {
        playSound (sound) {
        if(sound) {
            var audio = new Audio(sound);
            audio.play();
        }
        }
    }
    });
</script>