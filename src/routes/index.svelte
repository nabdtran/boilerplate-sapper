<svelte:head>
  <title>Sapper project template</title>
</svelte:head>

<script>
 import { onMount, afterUpdate } from 'svelte';

  let status = 'FROZEN';

  // Change status to fetch 2 seconds after mount
  onMount(() => {
    setTimeout(() => {
      status = 'FETCHING';
    }, 2000);
  });

  // Set status to `READY` 2 seconds after `FETCHING` status
  afterUpdate(() => {
    if ('FETCHING' === status) {
      setTimeout(() => {
        status = 'READY';
      }, 2000);
    }
  });
</script>

<main>
 {#if 'READY' === status}
    <h1>Great success!</h1>

<figure>
  <img alt="Borat" src="great-success.png" />
  <figcaption>HIGH FIVE!</figcaption>
</figure>

<p><strong>Ready to start blogging.</strong></p>
  {:else if 'FETCHING' === status}
    <div class="progress center" />
  {:else}
    <h1>Initiating</h1>
  {/if}

</main>

<style>
  h1,
  figure,
  p {
    text-align: center;
    margin: 0 auto;
  }

  h1 {
    font-size: 2.8em;
    text-transform: uppercase;
    font-weight: 700;
    margin: 0 0 0.5em 0;
  }

  figure {
    margin: 0 0 1em 0;
  }

  img {
    width: 100%;
    max-width: 400px;
    margin: 0 0 1em 0;
  }

  p {
    margin: 1em auto;
  }
  .center {
		display: flex;
		height: 100%;
		align-items: center;
		justify-content: center;
		flex-direction: column;
	}

  .progress {
    width:120px;
    height:20px;
    border-radius: 20px;
    background:
    repeating-linear-gradient(135deg,#f03355 0 10px,#ffa516 0 20px) left/0%   100% no-repeat,
    repeating-linear-gradient(135deg,#ddd    0 10px,#eee    0 20px) left/100% 100%;
    animation:p3 2s infinite;
  }
@keyframes p3 {
    100% {background-size:100% 100%}
}

  @media (min-width: 480px) {
    h1 {
      font-size: 4em;
    }
  }
</style>
