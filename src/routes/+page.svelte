<script>
	import logo from "$lib/images/Imagen2.png";
	import { getContext } from "svelte";
	import Tareas from "./tareas.svelte";
	const cambiarFondo = getContext('cambiarFondo');
	let CambiarIcono = false;
	let valorInput = '';
	let campos = [];
	function SiCambiaFondo()
	{
		cambiarFondo();
		cambiarIcon();
	}
	function cambiarIcon()
	{
		CambiarIcono = !CambiarIcono;
	}
	
	function AgregarElementos()
	{
		const nuevoTexto= valorInput.trim();
		if(nuevoTexto && !campos.some(campo => campo.texto === nuevoTexto))
		{
			campos = [...campos, { texto: nuevoTexto, editar: false, tachar: false}];
			valorInput ='';
		}
		else if (campos.some(campo => campo.texto === nuevoTexto))
		{
			alert ('Este campo ya existe');
		}
	}
	function cuandoEnter(event)
	{
		if(event.key === 'Enter')
		{
			AgregarElementos();
		}
	}

</script>
	<div class="container-">
		<div class="img position-relative mb-3">
			<img
				src={logo}
				class="img-fluid bg-primary"
				style="--bs-bg-opacity: .5;"
				alt="..."
			/>
			<button
				on:click={SiCambiaFondo}
				type="button"
				class="btn btn-outline-secondary position-absolute top-0 start-0 m-3 "
			>
			<h1><i class="fa-solid fa-sun {CambiarIcono ? 'fa-sun' : 'fa-moon'}"></i></h1>
			</button>
			<div
				class="input-group flex-nowrap position-absolute top-100 start-50 translate-middle w-50"
			>
				<input
					type="text"
					class="form-control"
					placeholder="Digite la tarea"
					aria-label="Username"
					aria-describedby="addon-wrapping"
					bind:value={valorInput}
					on:keydown={cuandoEnter}
				/>
				
			</div>
		</div>	
	</div>
	
	<Tareas bind:campos={campos} />
