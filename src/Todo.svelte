<script>
  export let todos
  export let todo
  let isEdit = false
  let title = ''

  const onEdit = () => {
    isEdit = true
    title = todo.title
  }

  const offEdit = () => {
    isEdit = false
  }

  const updateTodo = () => {
    todo.title = title
    offEdit()
  }

  const deleteTodo = () => {
    $todos = $todos.filter(({ id }) => id !== todo.id)
  }
</script>

{#if isEdit}
  <div>
    <input
      type="text"
      bind:value={title}
      on:keydown={({ key }) => key === 'Enter' && updateTodo()}
    />
    <button on:click={updateTodo}>OK</button>
    <button on:click={offEdit}>Cancel</button>
  </div>
{:else}
  <div>
    {todo.title}
    <button on:click={onEdit}>Edit</button>
    <button on:click={deleteTodo}>Delete</button>
  </div>
{/if}
