<script>
  import List from "./components/List.svelte";
  import Input from "./components/Input.svelte";

  let todos = [];
  function addItem(e) {
    todos = [...todos, e.detail];
  }

  function removeItem(event) {
    todos = todos.filter(t => t.title !== event.detail.title);
  }

  function itemDone(event) {
    if (event.detail.done) return;
    todos = todos.map(t => {
      if (t.title === event.detail.title) {
        return {
          ...t,
          done: true
        };
      }
      return {
        ...t
      };
    });
  }
</script>

<style>
  main {
    text-align: center;
    margin: 0 auto;
    background-color: #d1d8e0;
    height: 100vh;
  }

  .todo-container {
    display: flex;
    flex-flow: row wrap;
    justify-content: space-around;
    align-items: center;
    padding: 0 50px;
    height: 100%;
  }
</style>

<main>
  <div class="todo-container">
    <Input on:add={addItem} />
    <List {todos} on:remove={removeItem} on:done={itemDone} />
  </div>
</main>
