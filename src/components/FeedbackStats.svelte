<script>
  import { FeedbackStore } from "../stores";

  $: count = $FeedbackStore.length;
  $: average =
    $FeedbackStore.reduce((acc, item) => acc + item.rating, 0) /
    $FeedbackStore.length;
</script>

<div class="feedback-stats">
  <h4>{count} Reviews</h4>
  <h4>Ratings average: {average}</h4>
</div>

<style>
  .feedback-stats {
    display: flex;
    justify-content: space-between;
    margin: 20px 0;
  }
  .feedback-stats h4 {
    color: white;
  }
</style>
