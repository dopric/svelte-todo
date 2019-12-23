<script>
  import TodoItem from "./TodoItem.svelte";

  let title = "";

  let todoItems = [
    { title: "Learn Svelte", done: false, id: 1 },
    { title: "Go Shopping", done: false, id: 2 },
    { title: "Paint the Bathroom", done: false, id: 3 },
    { title: "Drink coffee", done: true, id: 4 }
  ];

  function toggleItem(event) {
    let item = todoItems.find(e => e.id === event.detail);
    item.done = !item.done;
    todoItems = [...todoItems, item];
  }
  function onTitleChanged(event) {
    let item = todoItems.find(e => e.id === event.detail.id);

    item.title = event.detail.title;
    todoItems = [...todoItems, item];
  }

  function addTodo() {
    if (title.length <= 0) {
      return;
    }
    todoItems = [
      { id: todoItems.length + 1, done: false, title: title },
      ...todoItems
    ];
    title = "";
  }
</script>

<div class="container">
  <h1>TodoList</h1>
  <form>
    <div class="form-group">
      <label for="todoText">Title</label>
      <input type="text" id="todoText" bind:value={title} />
      <button type="submit" on:click|preventDefault={addTodo}>
        Add new Todo
      </button>
    </div>
  </form>
  {#each todoItems as item (item.id)}
    <TodoItem
      value={item.title}
      done={item.done}
      id={item.id}
      on:doneToggled={toggleItem}
      on:titleChanged={onTitleChanged} />
  {/each}

</div>
