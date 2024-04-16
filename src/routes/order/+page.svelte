<script lang="ts">
  import { onMount } from 'svelte';
  import OrderCard from './OrderCard.svelte';

  let listdata: Array<any> = []; // Especifica el tipo de 'listdata' como un array de cualquier tipo

  onMount(async () => {
      const response = await fetch("https://backecommerse.netlify.app//.netlify/functions/server/order");
      
      const results = await response.json();
      listdata = results;
  });
</script>

<svelte:head>
  <title>Orden</title>
  <meta name="description" content="FullStack Wiz E-Commerce Store" />
</svelte:head>

<div class="padding-x pb-16 bg-fw-grey">
  {#each listdata as order}
    <OrderCard order={order} />
  {/each}
</div>
