<script>
import { setContext } from 'svelte';
import '../app.css';
let fon_negro = false;
function cambiarFondo()
{
    fon_negro= !fon_negro;
}
setContext('cambiarFondo', cambiarFondo);
</script>
    

<body class={fon_negro ? 'negro' : 'blanco'}>
    <div class="app">
        <main>
           <slot />
        </main>
    </div>  
</body>
<style>
    body
    {
        width: 100%;
        height: 100vh;
        margin: 0;
        transition: background 0.5s ease;   
    }
    .blanco
    {
        background:white;
        color: black;
    }
    .negro
    {
        background: black;       
    }
   
</style>