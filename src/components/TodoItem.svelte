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
  .done1 {
    text-decoration: line-through;
  }
  i.chk{
      float: left;
  }
</style>

<span>
  <input class="chk" type="checkbox" checked={done} on:click={doneToggled} />
  <input type="text" class:done1={done} bind:value={value} on:change={titleChanged}/>
</span><br/>
