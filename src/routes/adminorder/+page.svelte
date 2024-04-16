<script lang="ts">
  import { onMount } from 'svelte';
  import OrderCard from './OrderCard.svelte';
  import CreateOrderForm from './CreateOrderForm.svelte';
  import EditOrderForm from './EditOrderForm.svelte';
  import DeleteOrderForm from './DeleteOrderForm.svelte';

  let listdata: Array<any> = [];
  let activeForm: string | null = null;
  let selectedOrder: any = null;

  onMount(async () => {
      const response = await fetch("https://backecommerse.netlify.app//.netlify/functions/server/order");
      const results = await response.json();
      listdata = results;
  });

  function handleEdit(order: any) {
    activeForm = 'edit';
    selectedOrder = order;
  }

  function handleDelete(order: any) {
    activeForm = 'delete';
    selectedOrder = order;
  }

  function handleCreate() {
    activeForm = 'create';
    selectedOrder = null; // Reiniciamos el producto seleccionado al crear
  }

  function handleCancel() {
    activeForm = null;
    selectedOrder = null;
  }
</script>

<svelte:head>
  <title>AdminOrden</title>
  <meta name="description" content="FullStack Wiz E-Commerce Store" />
</svelte:head>

<style>
  .container {
    display: flex;
    flex-direction: column; /* Cambiar a disposición vertical */
  }

  .info,
  .form {
    padding: 0 20px; /* Agregar espaciado a los lados */
    margin-bottom: 20px; /* Agregar espacio entre las filas */
  }

  .info {
    border-bottom: 1px solid #ccc; /* Línea divisoria entre las filas */
  }

  @media (min-width: 768px) {
    .container {
      flex-direction: row; /* Cambiar a disposición horizontal en pantallas grandes */
    }

    .info,
    .form {
      flex: 1; /* Hacer que ocupen el mismo espacio */
      padding: 0 20px; /* Mantener el espaciado lateral */
      margin-bottom: 0; /* No agregar espacio entre las filas */
    }

    .info {
      border-bottom: none; /* Quitar la línea divisoria */
      border-right: 1px solid #ccc; /* Agregar línea divisoria entre las columnas */
    }
  }
</style>

<div class="padding-x pb-16 bg-fw-grey">
  <div class="container">
    <div class="info">
      {#each listdata as order}
        <OrderCard
          order={order}
          handleEdit={handleEdit}
          handleDelete={handleDelete}
        />
      {/each}
    </div>
    <div class="form">
      {#if activeForm === 'edit' && selectedOrder}
        <EditOrderForm order={selectedOrder} on:cancel={handleCancel} />
      {:else if activeForm === 'delete' && selectedOrder}
        <DeleteOrderForm order={selectedOrder} on:cancel={handleCancel} />
      {:else if activeForm === 'create'}
        <CreateOrderForm on:cancel={handleCancel} />
      {/if}
      <div class="container">
        <div class="form">
          <button on:click={handleCreate}>Create</button>
        </div>
      </div>
    </div>
  </div>
</div>
