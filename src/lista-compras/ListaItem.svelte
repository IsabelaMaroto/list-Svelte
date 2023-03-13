<script>
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();

    export let descricao;
    export let comprado;
</script>


<div class="container-item">
    <label>
        <input type="checkbox" bind:checked={comprado}/>
        {descricao}
    </label>
    <button on:click={() => dispatch("itemremovido")}>Excluir</button>
</div>

<style>
    .container-item{
        display: flex;
        justify-content: space-between;
        padding: 1rem ;
        align-items: center;
        background-color:#5b7c5b;
        border-bottom: 1px solid hsl(0, 0%, 100%);
    }
    label{
        font-size: 1.2rem;
    }
    button{
        padding: 0.5rem;
        width: 5rem;
        background-color: hsl(16, 100%, 66%);
        color: hsl(0, 0%, 100%);
        border: none;
    }
    button:hover{
        background-color: hsl(16, 100%, 78%);
        cursor: pointer;
    }
    
</style>