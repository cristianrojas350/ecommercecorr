<script lang="ts">
  import { onMount } from 'svelte';
  import ProductCard from './ProductCard.svelte';
  import CreateProductForm from './CreateProductForm.svelte';
  import EditProductForm from './EditProductForm.svelte';
  import DeleteProductForm from './DeleteProductForm.svelte';

  let listdata: Array<any> = [];
  let activeForm: string | null = null;
  let selectedProduct: any = null;

  onMount(async () => {
      const response = await fetch("https://backecommerse.netlify.app//.netlify/functions/server/product");
      const results = await response.json();
      listdata = results;
  });

  function handleEdit(product: any) {
    activeForm = 'edit';
    selectedProduct = product;
  }

  function handleDelete(product: any) {
    activeForm = 'delete';
    selectedProduct = product;
  }

  function handleCreate() {
    activeForm = 'create';
    selectedProduct = null; // Reiniciamos el producto seleccionado al crear
  }

  function handleCancel() {
    activeForm = null;
    selectedProduct = null;
  }
</script>

<svelte:head>
  <title>AdminProduct</title>
  <meta name="description" content="ecommerce corr" />
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
      {#each listdata as product}
        <ProductCard
          product={product}
          handleEdit={handleEdit}
          handleDelete={handleDelete}
        />
      {/each}
    </div>
    <div class="form">
      {#if activeForm === 'edit' && selectedProduct}
        <EditProductForm product={selectedProduct} on:cancel={handleCancel} />
      {:else if activeForm === 'delete' && selectedProduct}
        <DeleteProductForm product={selectedProduct} on:cancel={handleCancel} />
      {:else if activeForm === 'create'}
        <CreateProductForm on:cancel={handleCancel} />
      {/if}
      <div class="container">
        <div class="form">
          <button on:click={handleCreate}>Create</button>
        </div>
      </div>
    </div>
  </div>
</div>
