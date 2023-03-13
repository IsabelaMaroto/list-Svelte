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

<h2>Lista de compras</h2>
<form on:submit|preventDefault={adicionarItem}>
    <input bind:this={inputEL}/>
    <button type="submit">Adicionar item</button>
</form>


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

<div>Itens pendentes: {itensPendentes}</div>