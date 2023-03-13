<script>
    import ListaItem from './ListaItem.svelte';

    let itens = JSON.parse(localStorage.getItem("lista-compras")) ?? [];


    $: {
        localStorage.setItem("lista-compras", JSON.stringify(itens));
    }

    $: itensPendentes = itens.filter(item => !item.comprado).length;
    let inputEL = null;

    function adicionarItem(){
        itens = [
            ...itens, {
                comprado: false,
                descricao: inputEL.value
            }
        ]
        inputEL.value = "";
    };

    function removerItem(item){
        itens = itens.filter(i => i !== item);
    };
</script>

<main>
    <h2>Lista de compras</h2>
    <form on:submit|preventDefault={adicionarItem}>
        <input bind:this={inputEL} placeholder="digite o seu item aqui"/>
        <button type="submit">Adicionar item</button>
    </form>
    
    <div class="lista">
        {#if itens.length === 0}
            <div>A lista está vazia.</div>
        {:else}
        {#each itens as item, i}
            <ListaItem 
            bind:comprado={item.comprado} 
            descricao={item.descricao}
            on:itemremovido = {() => removerItem(item)}
            />
        {/each} 
        {/if}
    </div>

    <div class="contador">Itens pendentes: {itensPendentes}</div>
    
</main>


<style>
    main{
        background-color:darkseagreen;
        padding: 2rem 0;
    }
    h2{
        text-align: center;
        font-size: 2rem ;
        margin-bottom: 1rem;
    }
    form{
        display: flex;
        justify-content: center;
        padding: 1rem;
        margin-bottom: 1rem;
    }
    input{
        width: 80%;
        padding: 0.5rem;
        background-color: hsl(60, 56%, 91%);
        border: none;
        margin-right: 0.3rem;
    }
    button{
        padding: 0.5rem;
        cursor: pointer;
        border: none;
        background-color: hsl(60, 56%, 91%);
        color: hsl(0, 0%, 50%);
    }
    button:hover{
        background-color: hsl(120, 15%, 42%);
        color: hsl(0, 0%, 100%);
    }
    .lista{
        padding: 1rem 0;
        width: 98%;
        margin: 0 auto;
    }
    .contador{
        text-align:center;
        font-size: 1.2rem;
        font-weight: bold;
        color: hsl(0, 1%, 20%);
    }
</style>