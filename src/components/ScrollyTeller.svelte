<script>
  import Scroller from "@sveltejs/svelte-scroller";
  import Map from "./Map.svelte";
  import Shots from "./shots.svelte";
  import { onMount } from 'svelte';
  import * as d3 from 'd3';

  let count, index, offset, progress;
  let showMap = false;
  let shotsIndex = 0;
  let screenWidth, screenHeight, onethirdScreenWidth, halfScreenHeight, adjustmentscreenwidth;




  

  $: {
    // Update map visibility based on the index
    showMap = index >= 1  && offset >= 0.50 && offset <= 0.58; // 0-based index, so section 3 corresponds to index 2
  }

 let shotData0304 = [];
 let shotData0405 = [];
 let shotData0506 = [];
 let shotData0607 = [];
 let shotData0708 = [];
 let shotData0809 = [];
 let shotData0910 = [];
 let shotData1011 = [];
 let shotData1112 = [];
 let shotData1213 = [];
 let shotData1314 = [];
 let shotData1415 = [];
 let shotData1516 = [];
 let shotData1617 = [];
 let shotData1718 = [];
 let shotData1819 = [];
 let shotData1920 = [];
 let shotData2021 = [];
 let shotData2122 = [];


 onMount(async () => {
      const margin = { top: 20, right: 20, bottom: 20, left: 20 };
      const width = window.innerWidth - margin.left - margin.right;
      const height = window.innerHeight - margin.top - margin.bottom;



      screenWidth = width;
      screenHeight = height;
      onethirdScreenWidth = screenWidth * .28;
      halfScreenHeight = screenHeight * .65;
      adjustmentscreenwidth = screenWidth * .125;


  const res0304 = await fetch('lebron_shots_2003-04.csv');
  const csv0304 = await res0304.text();
  shotData0304 = d3.csvParse(csv0304, d3.autoType)

  const res0405 = await fetch('lebron_shots_2004-05.csv');
  const csv0405 = await res0405.text();
  shotData0405 = d3.csvParse(csv0405, d3.autoType)

  const res0506 = await fetch('lebron_shots_2005-06.csv');
  const csv0506 = await res0506.text();
  shotData0506 = d3.csvParse(csv0506, d3.autoType)

  const res0607 = await fetch('lebron_shots_2006-07.csv');
  const csv0607 = await res0607.text();
  shotData0607 = d3.csvParse(csv0607, d3.autoType)

  const res0708 = await fetch('lebron_shots_2007-08.csv');
  const csv0708 = await res0708.text();
  shotData0708 = d3.csvParse(csv0708, d3.autoType)

  const res0809 = await fetch('lebron_shots_2008-09.csv');
  const csv0809 = await res0809.text();
  shotData0809 = d3.csvParse(csv0809, d3.autoType)

  const res0910 = await fetch('lebron_shots_2009-10.csv');
  const csv0910 = await res0910.text();
  shotData0910 = d3.csvParse(csv0910, d3.autoType)

  const res1011 = await fetch('lebron_shots_2010-11.csv');
  const csv1011 = await res1011.text();
  shotData1011 = d3.csvParse(csv1011, d3.autoType)

  const res1112 = await fetch('lebron_shots_2011-12.csv');
  const csv1112 = await res1112.text();
  shotData1112 = d3.csvParse(csv1112, d3.autoType)

  const res1213 = await fetch('lebron_shots_2012-13.csv');
  const csv1213 = await res1213.text();
  shotData1213 = d3.csvParse(csv1213, d3.autoType)

  const res1314 = await fetch('lebron_shots_2013-14.csv');
  const csv1314 = await res1314.text();
  shotData1314 = d3.csvParse(csv1314, d3.autoType)

  const res1415 = await fetch('lebron_shots_2014-15.csv');
  const csv1415 = await res1415.text();
  shotData1415 = d3.csvParse(csv1415, d3.autoType)

  const res1516 = await fetch('lebron_shots_2015-16.csv');
  const csv1516 = await res1516.text();
  shotData1516 = d3.csvParse(csv1516, d3.autoType)

  const res1617 = await fetch('lebron_shots_2016-17.csv');
  const csv1617 = await res1617.text();
  shotData1617 = d3.csvParse(csv1617, d3.autoType)

  const res1718 = await fetch('lebron_shots_2017-18.csv');
  const csv1718 = await res1718.text();
  shotData1718 = d3.csvParse(csv1718, d3.autoType)

  const res1819 = await fetch('lebron_shots_2018-19.csv');
  const csv1819 = await res1819.text();
  shotData1819 = d3.csvParse(csv1819, d3.autoType)

  const res1920 = await fetch('lebron_shots_2019-20.csv');
  const csv1920 = await res1920.text();
  shotData1920 = d3.csvParse(csv1920, d3.autoType)

  const res2021 = await fetch('lebron_shots_2020-21.csv');
  const csv2021 = await res2021.text();
  shotData2021 = d3.csvParse(csv2021, d3.autoType)

  const res2122 = await fetch('lebron_shots_2021-22.csv');
  const csv2122 = await res2122.text();
  shotData2122 = d3.csvParse(csv2122, d3.autoType)
 });

  //let filteredShots0304 = shotData.filter(shot => shot.season === "2003-04");

  //shots0304 = shotData.filter(shot => shot.season === "2003-04");
  //console.log(shots0304);
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

<svg width=800 height=800>
  {#each shotData0304 as shot}
    <circle cx={shot.shotX*15} cy={shot.shotY*15} r=3/>
  {/each}
</svg>

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
    <Map/>
  {:else}
    <Shots /> 
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
    <section>
      2003-04
      {#if index === 1 && offset >= 0.50 && offset <= 0.58}
      <svg width={onethirdScreenWidth* 2} height={halfScreenHeight}>
        {#each shotData0304 as shot}
        <circle cx={shot.shotX*(onethirdScreenWidth / 800)*15 + (adjustmentscreenwidth)} cy={shot.shotY*(halfScreenHeight / 800)*15} r={3 * (onethirdScreenWidth / 800)}/>
        {/each}
      </svg>
      {/if}
    </section>
    <section>
      2004-05
      {#if index === 2 && offset >= 0.50 && offset <= 0.58}
      <svg width={onethirdScreenWidth* 2} height={halfScreenHeight}>
        {#each shotData0405 as shot}
        <circle cx={shot.shotX*(onethirdScreenWidth / 800)*15 + (adjustmentscreenwidth)} cy={shot.shotY*(halfScreenHeight / 800)*15} r={3 * (onethirdScreenWidth / 800)}/>
        {/each}
      </svg>
      {/if}
    </section>
    <section>
      2005-06
      {#if index === 3 && offset >= 0.50 && offset <= 0.58}
      <svg width={onethirdScreenWidth* 2} height={halfScreenHeight}>
        {#each shotData0506 as shot}
        <circle cx={shot.shotX*(onethirdScreenWidth / 800)*15 + (adjustmentscreenwidth)} cy={shot.shotY*(halfScreenHeight / 800)*15} r={3 * (onethirdScreenWidth / 800)}/>
        {/each}
      </svg>
      {/if}
    </section>
    <section>
      2006-07
      {#if index === 4 && offset >= 0.50 && offset <= 0.58}
      <svg width={onethirdScreenWidth* 2} height={halfScreenHeight}>
        {#each shotData0607 as shot}
        <circle cx={shot.shotX*(onethirdScreenWidth / 800)*15 + (adjustmentscreenwidth)} cy={shot.shotY*(halfScreenHeight / 800)*15} r={3 * (onethirdScreenWidth / 800)}/>
        {/each}
      </svg>
      {/if}
    </section>
    <section>
      2007-08
      {#if index === 5 && offset >= 0.50 && offset <= 0.58}
      <svg width={onethirdScreenWidth* 2} height={halfScreenHeight}>
        {#each shotData0708 as shot}
        <circle cx={shot.shotX*(onethirdScreenWidth / 800)*15 + (adjustmentscreenwidth)} cy={shot.shotY*(halfScreenHeight / 800)*15} r={3 * (onethirdScreenWidth / 800)}/>
        {/each}
      </svg>
      {/if}
    </section>
    <section>
      2008-09
      {#if index === 6 && offset >= 0.50 && offset <= 0.58}
      <svg width={onethirdScreenWidth* 2} height={halfScreenHeight}>
        {#each shotData0809 as shot}
        <circle cx={shot.shotX*(onethirdScreenWidth / 800)*15 + (adjustmentscreenwidth)} cy={shot.shotY*(halfScreenHeight / 800)*15} r={3 * (onethirdScreenWidth / 800)}/>
        {/each}
      </svg>
      {/if}
    </section>
    <section>
      2009-10
      {#if index === 7 && offset >= 0.50 && offset <= 0.58}
      <svg width={onethirdScreenWidth* 2} height={halfScreenHeight}>
        {#each shotData0910 as shot}
        <circle cx={shot.shotX*(onethirdScreenWidth / 800)*15 + (adjustmentscreenwidth)} cy={shot.shotY*(halfScreenHeight / 800)*15} r={3 * (onethirdScreenWidth / 800)}/>
        {/each}
      </svg>
      {/if}
    </section>
    <section>
      2010-11
      {#if index === 8 && offset >= 0.50 && offset <= 0.58}
      <svg width={onethirdScreenWidth* 2} height={halfScreenHeight}>
        {#each shotData1011 as shot}
        <circle cx={shot.shotX*(onethirdScreenWidth / 800)*15 + (adjustmentscreenwidth)} cy={shot.shotY*(halfScreenHeight / 800)*15} r={3 * (onethirdScreenWidth / 800)}/>
        {/each}
      </svg>
      {/if}
    </section>
    <section>
      2011-12
      {#if index === 9 && offset >= 0.50 && offset <= 0.58}
      <svg width={onethirdScreenWidth* 2} height={halfScreenHeight}>
        {#each shotData1112 as shot}
        <circle cx={shot.shotX*(onethirdScreenWidth / 800)*15 + (adjustmentscreenwidth)} cy={shot.shotY*(halfScreenHeight / 800)*15} r={3 * (onethirdScreenWidth / 800)}/>
        {/each}
      </svg>
      {/if}
    </section>
    <section>
      2012-13
      {#if index === 10 && offset >= 0.50 && offset <= 0.58}
      <svg width={onethirdScreenWidth* 2} height={halfScreenHeight}>
        {#each shotData1213 as shot}
        <circle cx={shot.shotX*(onethirdScreenWidth / 800)*15 + (adjustmentscreenwidth)} cy={shot.shotY*(halfScreenHeight / 800)*15} r={3 * (onethirdScreenWidth / 800)}/>
        {/each}
      </svg>
      {/if}
    </section>
    <section>
      2013-14
      {#if index === 11 && offset >= 0.50 && offset <= 0.58}
      <svg width={onethirdScreenWidth* 2} height={halfScreenHeight}>
        {#each shotData1314 as shot}
        <circle cx={shot.shotX*(onethirdScreenWidth / 800)*15 + (adjustmentscreenwidth)} cy={shot.shotY*(halfScreenHeight / 800)*15} r={3 * (onethirdScreenWidth / 800)}/>
        {/each}
      </svg>
      {/if}
    </section>
    <section>
      2014-15
      {#if index === 12 && offset >= 0.50 && offset <= 0.58}
      <svg width={onethirdScreenWidth* 2} height={halfScreenHeight}>
        {#each shotData1415 as shot}
        <circle cx={shot.shotX*(onethirdScreenWidth / 800)*15 + (adjustmentscreenwidth)} cy={shot.shotY*(halfScreenHeight / 800)*15} r={3 * (onethirdScreenWidth / 800)}/>
        {/each}
      </svg>
      {/if}
    </section>
    <section>
      2015-16
      {#if index === 13 && offset >= 0.50 && offset <= 0.58}
      <svg width={onethirdScreenWidth* 2} height={halfScreenHeight}>
        {#each shotData1516 as shot}
        <circle cx={shot.shotX*(onethirdScreenWidth / 800)*15 + (adjustmentscreenwidth)} cy={shot.shotY*(halfScreenHeight / 800)*15} r={3 * (onethirdScreenWidth / 800)}/>
        {/each}
      </svg>
      {/if}
    </section>
    <section>
      2016-17
      {#if index === 14 && offset >= 0.50 && offset <= 0.58}
      <svg width={onethirdScreenWidth* 2} height={halfScreenHeight}>
        {#each shotData1617 as shot}
        <circle cx={shot.shotX*(onethirdScreenWidth / 800)*15 + (adjustmentscreenwidth)} cy={shot.shotY*(halfScreenHeight / 800)*15} r={3 * (onethirdScreenWidth / 800)}/>
        {/each}
      </svg>
      {/if}
    </section>
    <section>
      2017-18
      {#if index === 15 && offset >= 0.50 && offset <= 0.58}
      <svg width={onethirdScreenWidth* 2} height={halfScreenHeight}>
        {#each shotData1718 as shot}
        <circle cx={shot.shotX*(onethirdScreenWidth / 800)*15 + (adjustmentscreenwidth)} cy={shot.shotY*(halfScreenHeight / 800)*15} r={3 * (onethirdScreenWidth / 800)}/>
        {/each}
      </svg>
      {/if}
    </section>
    <section>
      2018-19
      {#if index === 16 && offset >= 0.50 && offset <= 0.58}
      <svg width={onethirdScreenWidth* 2} height={halfScreenHeight}>
        {#each shotData1819 as shot}
        <circle cx={shot.shotX*(onethirdScreenWidth / 800)*15 + (adjustmentscreenwidth)} cy={shot.shotY*(halfScreenHeight / 800)*15} r={3 * (onethirdScreenWidth / 800)}/>
        {/each}
      </svg>
      {/if}
    </section>
    <section>
      2019-20
      {#if index === 17 && offset >= 0.50 && offset <=0.58}
      <svg width={onethirdScreenWidth* 2} height={halfScreenHeight}>
        {#each shotData1920 as shot}
        <circle cx={shot.shotX*(onethirdScreenWidth / 800)*15 + (adjustmentscreenwidth)} cy={shot.shotY*(halfScreenHeight / 800)*15} r={3 * (onethirdScreenWidth / 800)}/>
        {/each}
      </svg>
      {/if}
    </section>
    <section>
      2020-21
      {#if index === 18 && offset >= 0.50 && offset <= 0.58}
      <svg width={onethirdScreenWidth* 2} height={halfScreenHeight}>
        {#each shotData2021 as shot}
        <circle cx={shot.shotX*(onethirdScreenWidth / 800)*15 + (adjustmentscreenwidth)} cy={shot.shotY*(halfScreenHeight / 800)*15} r={3 * (onethirdScreenWidth / 800)}/>
        {/each}
      </svg>
      {/if}
    </section>
    <section>
      2021-22
      
      {#if index === 19 && offset >= 0.50 && offset <=0.58}
      <svg width={onethirdScreenWidth* 2} height={halfScreenHeight}>
        {#each shotData2122 as shot}
        <circle cx={shot.shotX*(onethirdScreenWidth / 800)*15 + (adjustmentscreenwidth)} cy={shot.shotY*(halfScreenHeight / 800)*15} r={3 * (onethirdScreenWidth / 800)}/>
        {/each}
      </svg>
      {/if}
    </section>
  </div>
</Scroller>