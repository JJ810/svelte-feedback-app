<script>
  import { createEventDispatcher } from "svelte";
  import Card from "./Card.svelte";
  export let item;

  const dispatch = createEventDispatcher();

  const removeFeedback = (id) => {
    dispatch("delete-feedback", id);
  };
</script>

<Card>
  <div class="num-display">
    {item.rating}
  </div>
  <button class="close" on:click={() => removeFeedback(item.id)}> X </button>
  <p class="text-display">
    {item.text}
  </p>
</Card>

<style>
  .num-display {
    font-size: 2rem;
    font-weight: bold;
    color: #333;
  }

  .close {
    font-size: 1.5rem;
    color: red;
    cursor: pointer;
    position: absolute;
    right: 1rem;
    top: 1rem;
    background: none;
    border: none;
    z-index: 999;
  }

  .text-display {
    font-size: 1rem;
    color: #333;
  }
</style>
