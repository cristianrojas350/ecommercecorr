<script lang="ts">
    
  export let handleEdit: (product: any) => void;
  export let handleDelete: (product: any) => void;
    export let product: {
      name: string;
      price: number;
      stock: number;
    } = {
      name: '',
      price: 0,
      stock: 0
    };
  
    // Verifica si el producto está en stock
    function isInStock(stock: number): string {
      return stock > 0 ? 'Disponible' : 'Agotado';
    }
  </script>
  <div class="card-container">
    <div class="card">
      <h3>{product.name}</h3>
      <p>Precio: ${product.price}</p>
      <p>Stock: {isInStock(product.stock)}</p>
      <div class="buttons">
        <button on:click={() => handleEdit(product)}>Editar</button>
        <button on:click={() => handleDelete(product)}>Eliminar</button>
      </div>
    </div>
  </div>
  
<style>
    .card-container {
      display: flex;
      flex-wrap: wrap; /* Permite que las tarjetas se envuelvan cuando no haya suficiente espacio */
      gap: 20px; /* Espacio entre las tarjetas */
    }
  
    .card {
      flex: 1 0 250px; /* Las tarjetas tendrán un ancho mínimo de 250px y se ajustarán automáticamente */
      background-color: #fff;
      border-radius: 8px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
      padding: 16px;
      margin-bottom: 20px; /* Espacio entre las filas */
    }
  </style>
  