
import { popScopeId } from 'vue';

import { SliderNav } from '#build/components';

import { Card } from '#build/components';
<template>
    <div class="h-[100vh] bg-stone-600 pt-36 px-24">
        <!-- Cards wrapper -->
        <div class="w-full h-fit relative">
            <Card  
            :imgSrc="prevPic.src" 
            :text="prevPic.text"
            :index="0"
            />
            <Card  
            :imgSrc="nextPic.src" 
            :text="nextPic.text"
            :index="1"
            />
            <Card  
            :imgSrc="frontPic.src" 
            :text="frontPic.text"
            :index="2"
            />
        </div>
        <SliderNav 
        @on-next-click="setCurrentIndex()"
        class="absolute right-0 top-1/2 -translate-y-1/2 pr-40"
        />
    </div>
</template>

<script setup lang="ts">
interface IPic {
    text: string
    src: string
}


const imgs: IPic[] = reactive([
    {
        text: "Massaggi",
        src: "images/massage.jpg"
    },
    {
        text: "Meditazioni",
        src: "images/meditation.jpg"
    },
    {
        text: "Pilates",
        src: "images/pilates.jpg"
    },
])


let currentIndex: int = ref(0)
let frontPic: IPic = computed(() => imgs[currentIndex.value])

//L'immagine ultima
let prevPic: IPic = computed(() => imgs[currentIndex.value - 1] ?? imgs[imgs.length - 1])

//L'immagine dietro quella frontale
let nextPic: IPic = computed(() => imgs[currentIndex.value + 1] ?? imgs[0])

function setCurrentIndex(){
    if (imgs[currentIndex.value + 1]){
        currentIndex.value = currentIndex.value += 1
        return
    }
    currentIndex.value = 0
}


watch(currentIndex, (newIndex, oldIndex) => {
    
})
</script>

<style lang="scss" scoped>

</style>