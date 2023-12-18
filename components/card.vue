
import { Card } from '#build/components';

import { Transition } from 'vue';

import { transform } from '@vue/compiler-core';

<template>
    <!-- card -->
    <div ref="card" class="card wrapper rounded-[40px] overflow-hidden absolute " :class="props.position">
        <div class="w-full aspect-video bg-orange-200 relative shadow-lg shadow-stone-500  border-stone-500">
            <div class="absolute gradient w-full bottom-0 p-14">
                <h4 class="text-8xl text-slate-300">
                    {{ text }}
                </h4>
            </div>
            <NuxtImg 
            :src="props.imgSrc" 
            :class="'w-full h-full object-cover'"
            />
        </div>
    </div>
</template>

<script setup lang="ts">
const props = defineProps<{
    imgSrc: string,
    text: string,
    position: string
}>()

const emits = defineEmits<{
    onCardRender: [card: HTMLDivElement | null]
}>()

const card = ref<HTMLDivElement | null>(null)

onMounted(() => {
    
})

</script>

<style  scoped>



.gradient {
        background: rgb(8,1,9);
        background: linear-gradient(0deg, rgba(8,1,9,1) 0%, rgba(0,212,255,0) 84%);
}

.obscure::before {
        content: "";
        position: absolute;
        top: 0;
        right: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.496);
        z-index: 20;
    }

</style>