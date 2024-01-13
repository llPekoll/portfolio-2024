<script lang="ts">
    import { Canvas } from '@threlte/core'
    import Scene from './Scene.svelte'
    import { fly } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
    import exeriences from '$lib/components/exps.json'
    let showMenu = true;
    let section:string; 
    console.log(exeriences.exps)
    const disp = (sec:string) => {
        section = sec;
        showMenu = !showMenu;
        console.log(section)
    }
</script>
<div class="relative w-full h-full">

    <div class="absolute ">
        <h1 class="pt-20 pl-20 text-4xl font-thin text-orange-600">
            <span class="font-bold text-7xl"> Mepa Yohann.</span>
        </h1>
        <h2 class="-mt-1 text-orange-400 pl-[26.7rem] font-thin text-2xl">Developper</h2>
    </div>
    <div class="absolute flex justify-end w-1/2 overflow-scroll h-96 text-slate-400 bottom-20 right-20">
        {#if showMenu}
            <ul>
                <li class="font-thin hover:text-orange-200 transition ease-in-out" >
                    <button on:click={()=>disp('work')} class="text-2xl hover:text-orange-400" >
                        Work.
                    </button>
                </li>
                <li class="font-thin hover:text-orange-200 transition ease-in-out" >
                    <button on:click={()=>disp('experience')} class="text-2xl hover:text-orange-400" >
                        Experience.
                    </button>
                </li>
                <li class="font-thin hover:text-orange-200 transition ease-in-out" >
                    <button on:click={()=>disp('about')} class="text-2xl hover:text-orange-400" >
                        About.
                    </button>
                </li>
            </ul>
        {/if}
        {#if !showMenu}
            {#if section == 'work'}
                <div class="text-2xl" transition:fly={{duration: 300, x: 100, y: 500, opacity: 0.5, easing: quintOut }}>
                    <h1>Work</h1>
                    <p>Here is a list of my projects</p>
                </div>
            {:else if section == 'experience'}
                <div class="text-2xl">
                    <div>
                    {#each exeriences.exps as exp }
                        <div class="pb-8 grid grid-cols-4 gap-2">
                            <div class="pt-2 mr-2 text-sm text-slate-100">
                                {exp.time}
                            </div>
                            <div class="col-span-3">
                                <p class="font-bold text-slate-100">
                                    {exp.position}
                                    •
                                    <span class="text-base font-normal">
    
                                        {exp.company}
                                    </span>
                                </p>
                                <p class="text-sm">
                                    {@html exp.conent}
                                </p>
                            </div>
                        </div>
                    {/each}
                </div>
                </div>
            {:else if section == 'about'}
                <div class="flex justify-end">
                <p class="w-1/3 text-justify text-slate-400" in:fly={{ delay: 250,duration: 300, x: 10, opacity: 0.5, easing: quintOut }}>I'm a 20 years old french student in computer science. I'm currently in my second year of DUT (Diplôme Universitaire de Technologie) in computer science at the University of Bordeaux. I'm looking for an internship in web development for the next year.</p>
                </div>
            {/if}
    
        {/if}
    </div>
    {#if !showMenu}
        <div class="absolute flex justify-end overflow-scroll text-slate-400 bottom-10 right-20">
            <button on:click={()=>showMenu=true } class="text-2xl hover:text-cyan-400" >
                Back
            </button>
        </div>
        {/if}
    <Canvas>
        <Scene />    
    </Canvas>
</div>
