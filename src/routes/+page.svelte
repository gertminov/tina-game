<script lang="ts">
    import Check from "$lib/Check.svelte";
    import Question from "$lib/Question.svelte";
    import {words} from "../lib/words";
    import {fly} from "svelte/transition"
    import SegmentedInput from "../lib/SegmentedInput.svelte";
    import {goto} from "$app/navigation"

    let idx = 0

    // $: word = words[idx]
    let right = 0
    let input = ""
    let questions = words.map(word => word.question)
    let answers = words.map(word => word.answer)
    let curWord: string = words[idx].answer
    let curQuest = words[idx].question

    function increment() {
        const curInput = input.toLowerCase()
        if (curInput == curWord.toLowerCase()) {
            right++
        }
        idx += 1
        if (idx == words.length) {
            goto(`/finish?r=${right}&t=${words.length}`)
        }
        curWord = words[idx].answer
        curQuest = words[idx].question
    }
</script>

<div class="grow flex flex-col justify-center items-center gap-12">
    <div class="flex-1 flex flex-col justify-center content-center gap-4">
<!--        <p class="text-2xl text-white text-center">{right} of {words.length} correct</p>-->
        <h1 class="text-4xl text-white">{curQuest}</h1>
    </div>
        <div class="flex-1 flex items-center">
            {#each answers as word, index}
                {#if (index === idx)}
                    <div out:fly="{{x:-400, duration: 400}}" in:fly="{{x:400, duration: 400, delay:400}}">
                        <!--                    <Question word={word} bind:inputchars={input} />-->
                        <SegmentedInput {word} bind:code={input}/>
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
