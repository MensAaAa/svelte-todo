<script>
  import Item from "./Item.svelte";
  export let todos;
</script>

<style>
  .list {
    min-width: 500px;
  }
</style>

<div class="list">
  <h1>List</h1>
  {#each todos as item}
    <Item {item} on:remove on:done />
  {/each}
</div>
