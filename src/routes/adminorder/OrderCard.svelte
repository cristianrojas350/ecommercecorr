<script lang="ts">
    export let order: any;
    export let handleEdit: (order: any) => void;
    export let handleDelete: () => void;
  
    function isInStock(stock: number): string {
        return stock > 0 ? 'Disponible' : 'Agotado';
    }
</script>

<style>
    .card-container {
        margin-top: 2px;
        padding: 2px;
        display: flex;
        flex-wrap: wrap;
        gap: 20px;
    }

    .card {
        flex: 1 0 250px;
        background-color: #fff;
        border-radius: 8px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* Aquí se aplica el efecto de sombra */
        padding: 16px;
        margin-bottom: 20px;
    }

    .buttons {
        display: flex;
        justify-content: space-between;
        margin-top: 10px;
    }

    .buttons button {
        padding: 8px 16px;
        border: none;
        border-radius: 4px;
        cursor: pointer;
        transition: background-color 0.3s;
    }

    .buttons button:hover {
        background-color: #f0f0f0;
    }
</style>

<div class="card-container">
    <div class="card">
        <h3>Cliente: {order.customer}</h3>
        <p>Estado: {order.status}</p>
       
        <div class="buttons">
            <button on:click={() => handleEdit(order)}>Editar</button>
            <button on:click={handleDelete}>Eliminar</button>
        </div>
    </div>
</div>
