<script lang="ts">
    import { Canvas } from '@threlte/core'
    import Scene from './Scene.svelte'
    import { fly } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
    import infos from '$lib/components/infos.json'
    let showMenu = true;
    let section:string;
    infos.xps.reverse()
    const disp = (sec:string) => {
        section = sec;
        showMenu = !showMenu;
    }
</script>
<div class="relative w-full h-full">

    <div class="absolute ">
        <div class="sm:pt-20 sm:pl-20 pt-10 pl-10 text-right ">
            <h1 class="font-bold text-orange-600 text-2xl sm:text-7xl">
                Mepa Yohann.
            </h1>
            <h2 class="-mt-1 text-normal font-thin text-orange-400 sm:text-2xl">Developper</h2>
        </div>
    </div>
    <div class="absolute flex items-end justify-end w-5/6 sm:w-1/2 text-slate-200 sm:bottom-20 sm:right-20 bottom-10 right-5">
        {#if showMenu}
            <ul>
                <li class="font-thin hover:text-orange-200 transition ease-in-out" >
                    <button on:click={()=>disp('work')} class="text-2xl hover:text-orange-400" >
                        Personal Work.
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
                <!-- <li class="font-thin hover:text-orange-200 transition ease-in-out" >
                    <button on:click={()=>disp('links')} class="text-2xl hover:text-orange-400" >
                        Links.
                    </button>
                </li> -->
            </ul>
        {/if}
        {#if !showMenu}
            {#if section == 'work'}
                <div class="pb-5 text-2xl" transition:fly={{duration: 300, x: 100, y: 500, opacity: 0.5, easing: quintOut }}>
                    {#each infos.works as work }
                                <a class="block italic font-thin hover:underline hover:text-orange-400 text-slate-100 transition ease-in-out " href={work.link} target="_blank" rel="noopener noreferrer">
                                    -> {work.name}.
                                </a>
                    {/each}
                </div>
            {:else if section == 'experience'}
                <div class="overflow-scroll text-2xl h-96">
                    <div>
                        {#each infos.xps as exp }
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
                <div class="sm:ml-10">
                    <h3 class="text-2xl font-bold">{infos.about.title}</h3>
                    <p class="pb-5 text-justify text-slate-300 font-thin" in:fly={{ delay: 250,duration: 300, x: 10, opacity: 0.5, easing: quintOut }}>{@html infos.about.conent}</p>
                </div>
            <!-- {:else if section == 'links'}
                {#each infos.links as link }
                    <a class="block italic font-thin hover:underline hover:text-orange-400 text-slate-100 transition ease-in-out " href={link.link} target="_blank" rel="noopener noreferrer">
                        -> {@html link.icon} {link.name}.
                    </a>
                {/each} -->
            {/if}
        {/if}   
    </div>
    {#if !showMenu}
        <div class="absolute flex justify-end overflow-scroll text-slate-400 sm:bottom-10 sm:right-20 bottom-5 right-10">
            <button on:click={()=>showMenu=true } class="text-4xl italic font-bold text-orange-600 animate-pulse" >
                Back.
            </button>
        </div>
    {:else }
    <div class="absolute flex overflow-scroll text-slate-400 sm:bottom-10 sm:right-20 bottom-5 right-10">
    {#each infos.links as link }
        <a class="block italic font-thin hover:underline hover:text-orange-400 text-slate-100 transition ease-in-out mx-2" href={link.link} target="_blank" rel="noopener noreferrer ">
            {@html link.icon} 
        </a>
        
        {/each}
    </div>
    {/if}
    <div class="w-full h-full">
        <Canvas>
            <Scene />    
        </Canvas>
    </div>
</div>
