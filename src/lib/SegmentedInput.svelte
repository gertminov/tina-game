<script lang="ts">
    import QuestionTie from "./QuestionTie.svelte";

    export let word = ""
    let length = word.length
    let els: HTMLInputElement[] = []
    let values  = [word[0]]
    export let code = ''
    let defaultCSS = "h-12 w-12 sm:h-24 sm:w-24 text-3xl bg-white rounded-2xl text-center uppercase border-4 border-opacity-0"
    let rightCSS = "h-12 w-12 sm:h-24 sm:w-24 text-3xl bg-white rounded-2xl text-center uppercase border-4 border-green-600 border-opacity-100"
    let wrongCSS = "h-12 w-12 sm:h-24 sm:w-24 text-3xl bg-white rounded-2xl text-center uppercase border-4 border-red-600 border-opacity-100"

    $: {
            code = values.join("")
    }

    function handleMoveAndBackspace(e) {
        let targetIndex = +e.target.getAttribute('index')

        switch(e.keyCode) {
            case 39: //ArrowRight
                e.preventDefault()
                els[min((length - 1), targetIndex + 1)].focus()
                break
            case 37: //ArrowLeft
                e.preventDefault()
                els[max(0, targetIndex - 1)].focus()
                break
            case 8: //Backspace
                e.preventDefault()

                if (targetIndex <2) return

                // if curent cell is empty we want to backspace the previous cell
                if (!values[targetIndex] && values[targetIndex] != 0) {
                    els[max(0, targetIndex - 1)].focus()
                    values[targetIndex - 1] = null
                    updateCSS(els[targetIndex -1], targetIndex-1, values[targetIndex -1])
                } else {
                     values[targetIndex] = null
                    updateCSS(e.target, targetIndex, values[targetIndex])
                }
                break
        }
    }

    function handleKey(e) {
        if (e.keyCode == 8) return
        const index = e.target.getAttribute("index")
        values[index] = e.key
        const curChar = word[index];

        updateCSS(e.target, index, e.key)

        els[min((length - 1), +e.target.getAttribute('index') + 1)].focus();
    }


    function updateCSS(target: HTMLInputElement, index: number, fieldValue: string) {
        const curChar = word[index]
        if (!fieldValue) {
            target.setAttribute("class", defaultCSS)
        }
        if (fieldValue.toLowerCase() == curChar.toLowerCase()) {
            target.setAttribute("class", rightCSS);
        } else {
            target.setAttribute("class", wrongCSS);
        }
    }

    function range(length) {
        let arr = []

        for (let i = 0; i < length; i++) {
            arr.push(i)
        }

        return arr
    }

    function min(a, b) {
        if (a < b) return a
        return b
    }

    function max(a, b) {
        if (a > b) return a
        return b
    }
</script>

<section class="flex gap-2">
    {#each range(length) as index}
        {#if index === 0}
            <input type="text" on:keydown="{handleMoveAndBackspace}" on:keypress|preventDefault="{handleKey}"
                   bind:this="{els[index]}" bind:value="{values[index]}" index="{index}"
                   class={defaultCSS} disabled
            >
            {:else }
            <input type="text" on:keydown="{handleMoveAndBackspace}" on:keypress|preventDefault="{handleKey}"
                   bind:this="{els[index]}" bind:value="{values[index]}" index="{index}"
                   class={defaultCSS}
            >
            {/if}
    {/each}
</section>

<style>

    input:focus {
        border: 2px solid #5f91f0;
    }
    .input-wrapper {
        display: flex;
        justify-content: space-between;
        align-items: center;
        width: 100%;
    }

</style>