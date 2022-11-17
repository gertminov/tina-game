<script lang="ts">
    import Check from "$lib/Check.svelte";
    import Question from "$lib/Question.svelte";
    import {words} from "$lib/../lib/words";
    import {fly} from "svelte/transition"

    let idx = 0

    // $: word = words[idx]
    let right = 0
    let input = []
    let curWord:string = words[idx]
    function increment() {
        const curInput = input.join("").toLowerCase()
        if (curInput == curWord.toLowerCase()) {
            right++
        }
        idx += 1
        curWord = words[idx]
    }
</script>

<div class="grow flex flex-col justify-center items-center gap-12">
    <div class="flex-1 flex flex-col justify-center content-center">
        <p class="text-2xl text-white">{right} of {words.length} correct</p>
        <p>correct word {curWord}</p>
    </div>
    <div class="flex-1 flex items-center">
        {#each words as word, index}
            {#if (index === idx)}
                <div out:fly="{{x:-400, duration: 400}}" in:fly="{{x:400, duration: 400, delay:400}}">
                    <Question {word} bind:inputchars={input} />
                </div>
            {/if}
        {/each}
    </div>
    <div class="flex-1">
        <button on:click={increment} class="bg-red-400 rounded-full p-2 hover:scale-95">
            <Check cssClass="h-8 w-8 fill-white"/>
        </button>
    </div>
</div>
