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
<Canvas>
    <Scene />    
</Canvas>
<div class="fixed top-0">
    <h1 class="pt-20 pl-20 text-4xl font-thin text-orange-600">
        <span class="font-bold text-7xl"> Mepa Yohann.</span>
    </h1>
    <h2 class="-mt-1 text-xl italic text-orange-400 pl-[27.5rem]">Developper</h2>
</div>
<div class="fixed bottom-20 right-20 text-slate-400">
    {#if showMenu}
        <ul >
            <li class=" hover:text-cyan-500" >
                <button on:click={()=>disp('work')} class="text-2xl hover:text-cyan-400" >
                    Work
                </button>
            </li>
            <li class=" hover:text-cyan-500" >
                <button on:click={()=>disp('experience')} class="text-2xl hover:text-cyan-400" >
                    Experience 
                </button>
            </li>
            <li class=" hover:text-cyan-500" >
                <button on:click={()=>disp('about')} class="text-2xl hover:text-cyan-400" >
                    About 
                </button>
            </li>
        </ul>
    {/if}
    {#if !showMenu}
    <button on:click={()=>showMenu=true } class="text-2xl hover:text-cyan-400" >
        Back
    </button>
        {#if section == 'work'}
            <div class="text-2xl" transition:fly={{duration: 300, x: 100, y: 500, opacity: 0.5, easing: quintOut }}>
                <h1>Work</h1>
                <p>Here is a list of my projects</p>
            </div>
        {:else if section == 'experience'}
            <div class="text-2xl">
                {#each exeriences.exps as exp }
                    <div class="flex pb-8">
                        <div class="mr-2 text-slate-100 text-sm pt-2">
                            {exp.time}
                        </div>
                        <div>
                            <p class="text-slate-100 font-bold">
                                {exp.position}
                                •
                                <span class="font-normal text-base">

                                    {exp.company}
                                </span>
                            </p>
                            <p class="text-sm">
                                {exp.conent}
                            </p>
                        </div>
                    </div>
                {/each}
            </div>
        {:else if section == 'about'}
            <div class="flex justify-end">
            <p class="w-1/3 text-justify text-slate-400" in:fly={{ delay: 250,duration: 300, x: 10, opacity: 0.5, easing: quintOut }}>I'm a 20 years old french student in computer science. I'm currently in my second year of DUT (Diplôme Universitaire de Technologie) in computer science at the University of Bordeaux. I'm looking for an internship in web development for the next year.</p>
            </div>
        {/if}

    {/if}
</div>
