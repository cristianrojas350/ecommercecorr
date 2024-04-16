<script lang="ts">
    export let order: any;
  
    let formData = {
        customer: order.customer,
        status: order.status,
    };
  
    async function handleSubmit() {
      const response = await fetch(`https://backecommerse.netlify.app//.netlify/functions/server/order${order.id}`, {
        method: 'PUT',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(formData)
      });
  
      if (response.ok) {
        alert('order actualizado exitosamente');
        
        // Puedes realizar otras acciones después de enviar los datos, como limpiar el formulario o actualizar la lista de order
      } else {
        alert('Hubo un error al actualizar el order');
      }
    }
</script>

<style>
    form {
        max-width: 400px;
        margin: 0 auto;
    }

    label {
        display: block;
        margin-bottom: 10px;
    }

    input[type="text"],
    input[type="number"],
    textarea {
        width: 100%;
        padding: 8px;
        border: 1px solid #ccc;
        border-radius: 4px;
        box-sizing: border-box;
        margin-top: 5px;
        margin-bottom: 10px;
    }

    textarea {
        resize: vertical; /* Permite redimensionar verticalmente el textarea si es necesario */
    }

    button[type="submit"] {
        background-color: #4CAF50;
        color: white;
        padding: 10px 20px;
        border: none;
        border-radius: 4px;
        cursor: pointer;
    }

    button[type="submit"]:hover {
        background-color: #45a049;
    }
</style>

<form on:submit|preventDefault={handleSubmit}>
    <label>
        Nombre:
        <input type="text" bind:value={formData.customer} />
    </label>
    <label>
        Estado:
        <input type="text" bind:value={formData.status} />
    </label>

    <button type="submit">Guardar Cambios</button>
</form>
