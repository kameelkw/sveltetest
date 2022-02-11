<script>
  import { slide } from "svelte/transition"
  let newTodo = ""
  let id = 0
  let todos = [
    {
      id: id++,
      title: "Get up",
      done: true,
    },
    {
      id: id++,
      title: "Eat",
      done: true,
    },
    {
      id: id++,
      title: "Go with vinky and kozi and rume and mima",
      done: false,
    },
    {
      id: id++,
      title: "Clean floor",
      done: false,
    },
    {
      id: id++,
      title: "Pet pussi",
      done: true,
    },
  ]

  function addTodo() {
    if (newTodo === "") return

    todos = [
      {
        id: ++id,
        title: newTodo,
        done: false,
      },
      ...todos,
    ]
    newTodo = ""
  }

  function removeTodo(id) {
    todos = todos.filter(todo => todo.id !== id)
  }

  function clearCompleted() {
    todos = todos.filter(todo => !todo.done)
  }
</script>

<main>
  <h1>TODO</h1>
  <section class="add-todo">
    <input type="text" placeholder="task" bind:value={newTodo} />
    <button disabled={newTodo === ""} on:click={addTodo}>Add</button>
  </section>
  <section class="todos">
    {#each todos.filter(todo => !todo.done) as todo (todo.id)}
      <div transition:slide class="todo">
        <input type="checkbox" bind:checked={todo.done} name="complete task" />
        <input type="text" class:done={todo.done} bind:value={todo.title} />
        <button on:click={() => removeTodo(todo.id)}>x</button>
      </div>
    {/each}
    {#each todos.filter(todo => todo.done) as todo (todo.id)}
      <div transition:slide class="todo">
        <input type="checkbox" bind:checked={todo.done} name="complete task" />
        <input type="text" class:done={todo.done} bind:value={todo.title} />
        <button on:click={() => removeTodo(todo.id)}>x</button>
      </div>
    {/each}
  </section>
  <section>
    <button on:click={clearCompleted}>Remove completed</button>
  </section>
</main>

<style>
  h1 {
    text-align: center;
  }
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
  .todo input {
    border: none;
    background: rgb(250, 172, 183);
    color: black;
  }

  .todo input.done {
    opacity: 0.4;
    text-decoration: line-through;
  }
</style>
