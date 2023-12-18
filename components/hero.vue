
import { set } from 'nuxt/dist/app/compat/capi';

import { set } from 'nuxt/dist/app/compat/capi';

import cardVue from './card.vue';

import cardVue from './card.vue';

import cardVue from './card.vue';

import { popScopeId } from 'vue';

import { SliderNav } from '#build/components';

import { Card } from '#build/components';
<template>
    <div class="h-[100vh]  bg-stone-600 pt-48 px-32 isolate">
        <!-- Cards wrapper -->
        <div class="w-5/6 mx-auto  relative">
            <Card  v-for="img in imgs"
            :imgSrc="img.src" 
            :text="img.text"
            :position="img.position"
            />
            <SliderNav 
                @on-next-click="setCurrentIndex()"
                class="fixed right-[10%] top-1/2 -translate-y-1/2  z-10"/>
        </div>
    </div>
</template>

<script setup lang="ts">
import { gsap } from "gsap";

interface IPic {
    text: string
    src: string
    position: string
}


const imgs: IPic[] = reactive([
    {
        text: "Massaggi",
        src: "images/massage.jpg",
        position: "front",
    },
    {
        text: "Meditazioni",
        src: "images/meditation.jpg",
        position: "next"
    },
    {
        text: "Pilates",
        src: "images/pilates.jpg",
        position: "prev"
    },
])




let currentIndex = ref(0)

const setPositions = () => {
    let front: IPic = imgs[currentIndex.value]
    front.position = "front"

    let prev: IPic = imgs[currentIndex.value - 1] ?? imgs[imgs.length - 1]
    prev.position = "prev"

    let next = imgs[currentIndex.value + 1] ?? imgs[0]
    next.position = "next"

    // setAttrs()
}

function setCurrentIndex(){
    if (imgs[currentIndex.value + 1]){
        currentIndex.value = currentIndex.value += 1
        return
    }
    currentIndex.value = 0
}


function setAttrs() {
    gsap.set(".card.next", {yPercent: -15, scale: 0.9, zIndex: 2})
    gsap.set(".card.prev", {yPercent: -30, scale: 0.8, zIndex: 1})
    gsap.set(".card.front", {zIndex: 3})
}

const nextMotion = () => {
    const tl = gsap.timeline({duration: 1, ease: "power3.inOut", onComplete: () => setPositions()})
    tl.to(".card.front",{xPercent: 200, rotate: 60})
    tl.to(".card.next",{scale: 1, yPercent: 0, zIndex: 3}, "<")
    tl.to(".card.prev", {yPercent: -15, scale: 0.9, zIndex: 2}, "<.2")
    tl.to(".card.front",{xPercent: 0, yPercent: -30, rotate: 0,  zIndex: 1, scale: 0.8, opacity:1}, "<")
}

watch(currentIndex, () => {
    nextMotion()
})

onMounted(() => {
    setAttrs()
})

</script>

<style lang="scss" scoped>

</style>