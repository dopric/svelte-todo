<script>
  import { createEventDispatcher } from "svelte";

  export let value = "";
  export let done = false;
  export let id;

 
  const dispatcher = createEventDispatcher();

  function doneToggled() {
    dispatcher("doneToggled", id);
  }

  function titleChanged(){
      dispatcher('titleChanged', {id: id, title: value})
  }
</script>

<style>
  .doneTodo {
    text-decoration: line-through;
  }
</style>

<div>
  <input  type="checkbox" checked={done} on:click={doneToggled} />
  <input type="text" class:doneTodo={done} bind:value={value} on:change={titleChanged}/>
<br/>
</div>
