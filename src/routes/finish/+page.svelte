<script lang="ts">
    import {page} from "$app/stores"

    const right = $page.url.searchParams.get("r")
    const total = $page.url.searchParams.get("t")
    const good = "🐳"
    const bad = "🐸"
    const ok = "🐻"

    const rightInt = parseInt(right)
    const totalInt = parseInt(total)
    let emote = bad

    if (rightInt /totalInt > 0.7) {
        emote = good
    }else if (rightInt /totalInt > 0.4) {
        emote = ok
    }

</script>

<div class="grow grid place-content-center">
    <div class="text-6xl text-white text-center">
        <h1 class="my-4">Congrats {emote}</h1>
        <h1 class="">{right}/{total}</h1></div>
</div>
