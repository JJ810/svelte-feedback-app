<script>
  import { v4 as uuidv4 } from "uuid";
  import { createEventDispatcher } from "svelte";
  import Card from "./Card.svelte";
  import Button from "./Button.svelte";
  import RatingSelect from "./RatingSelect.svelte";

  let text = "";
  let rating = 10;
  let btnDisabled = true;
  let min = 10;
  let message;

  const handleInput = () => {
    if (text.trim().length > min) {
      message = null;
      btnDisabled = false;
    } else {
      message = `Please enter at least ${min} characters`;
      btnDisabled = true;
    }
  };

  const handleSelect = (e) => {
    rating = e.detail;
  };

  const reset = () => {
    text = "";
    rating = 10;
  };

  const dispatch = createEventDispatcher();
  const handleSubmit = () => {
    if (text.trim().length > 10) {
      const newFeedback = {
        id: uuidv4(),
        text,
        rating: +rating,
      };
      dispatch("add-feedback", newFeedback);
      reset();
    }
  };
</script>

<Card>
  <header>
    <h2>How would you rate your service with us? {rating}</h2>
  </header>
  <form on:submit|preventDefault={handleSubmit}>
    <RatingSelect on:rating-select={handleSelect} />
    <div class="input-group">
      <input
        type="text"
        placeholder="Tell us something that keeps you coming back"
        bind:value={text}
        on:input={handleInput}
      />
      <Button disabled={btnDisabled} type="submit">Send</Button>
    </div>
    {#if message}
      <div class="message">
        {message}
      </div>
    {/if}
  </form>
</Card>

<style>
  header {
    max-width: 400px;
    margin: auto;
  }

  header h2 {
    font-size: 22px;
    font-weight: 600;
    text-align: center;
  }

  .input-group {
    display: flex;
    flex-direction: row;
    border: 1px solid #ccc;
    padding: 8px 10px;
    border-radius: 8px;
    margin-top: 15px;
  }

  input {
    flex-grow: 2;
    border: none;
    font-size: 16px;
  }

  input:focus {
    outline: none;
  }

  .message {
    padding-top: 10px;
    text-align: center;
    color: rebeccapurple;
  }
</style>
