<script>
    import Title from "./Title.svelte";
    import Expense from "./Expense.svelte";
    import { identity } from "svelte/internal";

    export let expenses = [];
    export let removeExpense;
</script>

<section>
    <Title title="expenses list" />
    <ul>
        {#each expenses as expense, index}
        <!-- destructure expense to id, name, amount -->
            <li><Expense {...expense} {removeExpense} /></li>
        {:else}
            <h2>currently no expenses</h2>
        {/each}
    </ul>
</section>
