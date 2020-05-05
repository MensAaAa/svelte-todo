<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();
  let newTodo = "";
  function addItem() {
    if (newTodo === "") return;
    dispatch("add", { title: newTodo, done: false });
    newTodo = "";
  }
</script>

<style>
  .input-field {
    display: flex;
    flex-flow: column wrap;
  }

  label {
    font-weight: bold;
    text-align: left;
    margin-bottom: 10px;
    font-size: 14px;
  }

  input {
    width: 350px;
  }

  button {
    width: 150px;
    border-radius: 10px;
    border: 1px solid #3867d6;
    background-color: #3867d6;
    color: white;
    text-transform: uppercase;
    cursor: pointer;
    height: 40px;
  }
</style>

<div class="input-field">
  <label>Add item</label>
  <input bind:value={newTodo} />
  <button on:click={addItem}>Submit</button>
</div>
