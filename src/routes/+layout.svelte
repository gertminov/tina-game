<script>
  import "../app.css";
  import Header from "$lib/Header.svelte";
</script>

<div class="min-h-screen w-screen flex flex-col bg-blue-600 overflow-hidden">
    <Header/>
    <div class="grow flex flex-col">
        <slot></slot>
    </div>
</div>