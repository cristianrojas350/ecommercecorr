<script lang="ts">
    let formData = {
      name: '',
      subproduct: '',
      description: '',
      price: 0,
      category: '',
      stock: 0
    };
  
    async function handleSubmit() {
      const response = await fetch('https://backecommerse.netlify.app//.netlify/functions/server/product', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(formData)
      });
  
      if (response.ok) {
        alert('Producto creado exitosamente');
        // Puedes realizar otras acciones después de enviar los datos, como limpiar el formulario o actualizar la lista de productos
      } else {
        alert('Campos vacios');
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
    <h2> Formulario de Creacion Producto</h2>
    <label>
        Nombre:
        <input type="text" bind:value={formData.name} />
    </label>
    <label>
        Subproducto:
        <input type="text" bind:value={formData.subproduct} />
    </label>
    <label>
        Descripción:
        <textarea bind:value={formData.description}></textarea>
    </label>
    <label>
        Precio:
        <input type="number" step="0.01" bind:value={formData.price} />
    </label>
    <label>
        Categoría:
        <input type="text" bind:value={formData.category} />
    </label>
    <label>
        Stock:
        <input type="number" bind:value={formData.stock} />
    </label>
    <button type="submit">Crear Producto</button>
</form>
