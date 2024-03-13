<script>
  import Scroller from "@sveltejs/svelte-scroller";
  import Map from "./Map.svelte";

  let count, index, offset, progress;
  let showMap = false;

  $: {
    // Update map visibility based on the index
    showMap = index === 2; // 0-based index, so section 3 corresponds to index 2
  }

</script>

<style>
  .background {
    width: 100%;
    height: 100vh;
    position: relative;
    outline: none;
  }

  .foreground {
    width: 50%;
    margin: 0 auto;
    height: auto;
    position: relative;
    outline: none
  }

  .progress-bars {
    position: absolute;
    background: rgba(170, 51, 120, 0.2) /*  40% opaque */;
    visibility: visible;
  }

  section {
    height: 80vh;
    background-color: rgba(0, 0, 0, 0); /* 20% opaque */
    /* color: white; */
    outline: none;
    text-align: center;
    max-width: 750px; /* adjust at will */
    color: black;
    padding: 1em;
    margin: 0 0 2em 0;
  }
</style>

<Scroller
  top={0.0}
  bottom={1}
  threshold={0.5}
  bind:count
  bind:index
  bind:offset
  bind:progress

>
  <div class="background" slot="background">
    {#if showMap}
      <Map />
    {/if}

    <div class="progress-bars">
      <p>current section: <strong>{index + 1}/{count}</strong></p>
      <progress value={count ? (index + 1) / count : 0} />

      <p>offset in current section</p>
      <progress value={offset || 0} />

      <p>total progress</p>
      <progress value={progress || 0} />
    </div>
  </div>

  <div class="foreground" slot="foreground">
    <section>Lebron shooting throughout his career</section>
    <section></section>
    <section></section>
  </div>
</Scroller>