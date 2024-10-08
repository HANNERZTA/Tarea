<!-- portafolio de tareas -->
 <script>
    export let campos = [];
    function eliminarCampo(index)
    {
        campos = campos.filter((_, i) => i !== index);
    }
    function editarTexto(index)
    {
        campos[index].editar = !campos[index].editar;
    }
    function tacharTarea(index)
    {
        campos[index].tachar = !campos[index].tachar;
    }
 </script>

{#each campos as campo, index}
 <div class="tareas d-flex justify-content-center" >
    <div class="row border w-50 shadow p-2 bg-white rounded">
        <div class="col-md-1 ms-md-auto">
            <button 
            class= "tarea
            fa-solid  
            {campo.tachar ? 'fa-check':'fa-'}"
            on:click={() => tacharTarea(index)}
            >   
            </button>
        </div>
        <div class="col-md-9 ms-md-auto text-center">
            {#if campo.editar}
            <input 
                type="text" 
                bind:value={campo.texto} 
                on:blur={() => editarTexto(index)} 
            />
            {:else}
                 <label on:click={() => editarTexto(index)}>{campo.texto}</label>
            {/if}
        </div>
        <div class="col-md-1 ms-md-auto">
            <button 
            type="button" 
            class="btn-close" 
            aria-label="Cerrar" 
            on:click={() => eliminarCampo(index)}>
            </button>
        </div>
    </div>
</div>
{/each}    
<style>
    .tarea  
    {
        background: rgb(197, 197, 197);
        width: 25px;
        height: 25px;
        border-radius: 50%;
        border: transparent;
    }
    .fa-check
    {
        background: linear-gradient(45deg,#f1948a,#707b7c);
        width: 100%;
        height: 100%;
    }
</style>
