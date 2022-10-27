<script>
    import Title from "./Title.svelte";
    import Expense from "./Expense.svelte";

    export let expenses = [];
</script>

<section>
    <Title title="expenses list" />
    <ul>
        {#each expenses as expense}
            <!-- destructure expense to id, name, amount -->
            <li><Expense {...expense} /></li>
        {:else}
            <h2>Currently, you have no expenses</h2>
        {/each}
    </ul>
</section>
