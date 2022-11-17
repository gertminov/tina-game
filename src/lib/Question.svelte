<script lang="ts">

    import SegmentedInput from "./SegmentedInput.svelte";


    export let word = ""
    console.log(word)
    $: chars = word.split("")
    export let inputchars = Array(chars.length)
    let test = ""

</script>

<div class="flex gap-4">
    <!--{#each chars as char, index}-->
<!--        <QuestionTie {char} bind:val={inputchars[index]} {index} />-->
        <SegmentedInput length={word.length} bind:code={test}/>
    <!--{/each}-->
</div>
