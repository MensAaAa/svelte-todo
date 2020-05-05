<script>
  import { fade, fly } from "svelte/transition";
  import { createEventDispatcher } from "svelte";
  import { elasticOut } from "svelte/easing";

  export let item;
  const dispatch = createEventDispatcher();
  function removeItem(e) {
    e.preventDefault();
    dispatch("remove", item);
  }

  function itemDone(e) {
    e.preventDefault();
    dispatch("done", item);
  }

  function removeAnimation(node) {
    return {
      css: t => {
        const eased = elasticOut(t);
        return `
          transform: translateX(${eased * 100}px);
        `;
      }
    };
  }
</script>

<style>
  .item {
    display: flex;
    flex-flow: row wrap;
    justify-content: space-between;
    align-items: center;
    border: 1px solid #a5b1c2;
    background-color: white;
    padding: 10px;
  }

  .line span{
    text-decoration: line-through;
  }

  .buttons button {
    width: 120px;
    border: 1px solid;
    border-radius: 50px;
    color: white;
    cursor: pointer;
    margin: 0;
  }

  .buttons .delete {
    background-color: #eb3b5a;
  }

  .buttons .start {
    background-color: #20bf6b;
  }
</style>

<div class={`item ${item.done ? 'line' : ''}`} in:fly={{ y: 200, duration: 1000 }} out:removeAnimation>
  <span>{item.title}</span>
  <div class="buttons">
    <button class="start" on:click={itemDone}>{item.done ? 'Done' : 'Complete'}</button>
    <button class="delete" on:click={removeItem}>X</button>
  </div>
</div>
