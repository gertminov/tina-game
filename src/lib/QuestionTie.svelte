<script lang="ts">
    export let char = ""
    export let index: number
    let disabled = "disabled"
    export let val = ""
    if (index > 0) {
        val = "";
        disabled = "";
    } else {
        val = char
    }
    let opacity = "border-opacity-0";
    $:{
        if (val == "") {
            opacity = "border-opacity-0"
        } else if (val.toLowerCase() == char.toLowerCase() && index > 0) {
            opacity = "border-opacity-100 border-green-600";
        } else if (val.toLowerCase() != char.toLowerCase() && index > 0) {
            opacity = "border-opacity-100 border-red-600"
        }
    }

</script>

<input type="text" maxlength="1"
       class="h-12 w-12 sm:h-24 sm:w-24 text-3xl bg-white rounded-2xl text-center uppercase border-4 {opacity}"
       {disabled} bind:value={val}>