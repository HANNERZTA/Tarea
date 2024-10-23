<!-- portafolio de tareas -->
 <script>
    /**
     * @type {any[]}
     */
     export let campos = [];
     let filtro ='todo';
         /**
     * @param {number} index
     */
    function eliminarCampo(index)
    {
        campos = campos.filter((_, i) => i !== index);
    }
    /**
     * @param {number} index
     */
    function editarTexto(index)
    {
        campos[index].editar = !campos[index].editar;
    }
    /**
     * @param {number} index
     */
    function tacharTarea(index)
    {
        campos[index].tachar = !campos[index].tachar;
    }
    $: tareasFiltradas = campos.filter(campo => {
        if(filtro ==='todo') return true;
        if(filtro ==='pendientes') return !campo.tachar;
        if(filtro ==='completados') return campo.tachar;
        return true;
    });
    /**
     * @param {string} nuevoFiltro
     */
    function seleccionFiltro(nuevoFiltro){
        filtro = nuevoFiltro;
    }
 </script>

{#each tareasFiltradas as campo, index}
 <div class="tareas d-flex justify-content-center" >
    <div class="row border w-50 shadow p-2 bg-white rounded">
        <div class="col-md-1 w-10 h-auto">
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
                 <!-- svelte-ignore a11y-click-events-have-key-events -->
                 <!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
                 <!-- svelte-ignore a11y-label-has-associated-control -->
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
{#if campos.length < 1}
<p></p>
{:else}
<div class="filtro d-flex justify-content-center">
    <div class="d-flex border w-50 shadow  bg-white rounded">
        <div class="conteo mx-5 mt-2">
            <p>{campos.length} tareas</p>  
        </div>
        <div class="seleccion mx-5 mt-2 ">
            <!-- svelte-ignore a11y-invalid-attribute -->
            <a href="#" on:click|preventDefault={() => seleccionFiltro('todo')}>Todo</a>
            <!-- svelte-ignore a11y-invalid-attribute -->
            <a href="#" on:click|preventDefault={() => seleccionFiltro('pendientes')}>Pendiente</a>
            <!-- svelte-ignore a11y-invalid-attribute -->
            <a href="#" on:click|preventDefault={() => seleccionFiltro('completados')}>Completados</a>
        </div>
    </div>
</div>
{/if}
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
