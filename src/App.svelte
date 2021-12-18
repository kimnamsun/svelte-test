<script>
  import { writable } from 'svelte/store'
  import Todo from './Todo.svelte'
  let title = ''
  let todos = writable([])
  let id = 0

  const createTodo = () => {
    if (!title.trim()) {
      title = ''
      return
    }

    $todos.push({
      id: id++,
      title,
    })
    $todos = $todos
    title = ''
  }
</script>

<main>
  <input
    type="text"
    bind:value={title}
    on:keydown={({ key }) => key === 'Enter' && createTodo()}
  />
  <button on:click={createTodo}> Create Todo </button>

  {#each $todos as todo}
    <!-- <Todo bind:todos {todo} /> -->
    <Todo {todos} {todo} />
  {/each}
</main>
