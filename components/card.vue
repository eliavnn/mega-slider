
<template>
    <!-- card -->
    <div class="rounded-[40px] overflow-hidden absolute translate left-1/2">
        <div class="w-[700px] aspect-video bg-orange-200 relative shadow-lg shadow-stone-500  border-stone-500">
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
    index: number
}>()

const translatePx = computed(() => {
    return `${props.index * 90}px`
})

const scale = computed(() => {
    return  1 + parseFloat(`0.${props.index}`)
})

</script>

<style  scoped>
.translate {

    transform: translate(-50%, v-bind(translatePx)) scale(v-bind(scale));

}

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