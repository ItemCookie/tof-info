<script lang="ts">
    import SimulacraCard from "$lib/components/simulacra-card.svelte"
    import SimulacraGrid from "$lib/components/simulacra-grid.svelte"

    export let data;

    $: sorted = [...data.simulacras].sort((a, b) => {
        const rarityA = a.data.weapon.rarity;
        const rarityB = b.data.weapon.rarity;
        const rarity = (rarityB as string).length - (rarityA as string).length;
        const order = (b.data.order ?? 0) - (a.data.order ?? 0);
        return rarity || order;
    })
</script>

<svelte:head>
    <title>Simulacra | ToF Resources</title>
</svelte:head>

<SimulacraGrid>
    {#each sorted as {data: simulacra, name}}
        <SimulacraCard
            simulacra={name}
            name={simulacra.name}
            rarity={simulacra.weapon.rarity}
            resonance={simulacra.weapon.resonance}
            element={simulacra.weapon.element} />
    {/each}
</SimulacraGrid>
