<script lang="ts">
import { onMount } from "svelte";
import anime from "animejs";


export let nbCircles: number = 7;
export let title: string = "Projects";

let refCircles: HTMLDivElement[] = Array(nbCircles);

let duration = 1000;

let animeFn = async (c: HTMLDivElement) => anime({
            targets: c,
            easing: "linear",
            translateX: anime.random(-10, 10),
            translateY: anime.random(-10, 10),
            duration
        })
        .finished

onMount(async () => {
    for (let c of refCircles)
        animeFn(c)
    setInterval(async () => {
        for (let c of refCircles)
            await animeFn(c)
    }, duration)
    
});

</script>

<style>
    .circle {
        border: 1px solid red;
    }
</style>

<div class="relative w-40 h-40 flex align-middle justify-center items-center">
    {#each Array(nbCircles) as i, index}
        <div class="circle w-full h-full absolute rounded-full" style="transform: translate({anime.random(1, 10)}px, {anime.random(1,10)}px);" bind:this={refCircles[index]}></div>
    {/each}
    <div class="text-xl">
        {title}
    </div>
</div>