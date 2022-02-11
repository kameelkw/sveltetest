<script>
  let newTodo = ""
  let todos = [
    {
      title: "Get up",
      done: true,
    },
    {
      title: "Eat",
      done: true,
    },
    {
      title: "Go with vinky and kozi and rume and mima",
      done: false,
    },
    {
      title: "Clean floor",
      done: false,
    },
    {
      title: "Pet pussi",
      done: true,
    },
  ]

  function addTodo() {
    if (newTodo === "") return

    todos = [
      ...todos,
      {
        title: newTodo,
        done: false,
      },
    ]
    newTodo = ""
  }

  function removeTodo(i) {
    todos.splice(i, 1)
    todos = todos
  }
</script>

<main>
  <h1>TODO</h1>
  <section class="add-todo">
    <input type="text" placeholder="task" bind:value={newTodo} />
    <button disabled={newTodo === ""} on:click={addTodo}>Add</button>
  </section>
  <section class="todos">
    {#each todos as todo, i}
      <div class="todo">
        <input type="checkbox" bind:checked={todo.done} name="complete task" />
        <input type="text" disabled class:done={todo.done} value={todo.title} />
        <button on:click={() => removeTodo(i)}>x</button>
      </div>
    {/each}
  </section>
</main>

<style>
  .add-todo {
    display: grid;
    grid-template-columns: 1fr auto;
    gap: 0.5rem;
  }
  .todo {
    display: grid;
    grid-template-columns: auto 1fr auto;
    align-items: center;
    gap: 0.5rem;
  }
  input:disabled {
    border: none;
    background: lightpink;
    color: black;
  }

  input:disabled.done {
    opacity: 0.4;
    text-decoration: line-through;
  }
</style>
