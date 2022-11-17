<script lang="ts">

    import QuestionTie from "$lib/QuestionTie.svelte";

    export let word = ""
    $: chars = word.split("")
    export let inputchars = Array(chars.length)

</script>

<div class="flex gap-4">
    {#each chars as char, index}
        <QuestionTie {char} bind:val={inputchars[index]} {index} />
    {/each}
</div>
