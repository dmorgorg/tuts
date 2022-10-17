<script>
    // export let expense;
    // let { name, amount, id } = expense;
    // export let id;
    export let name = "";
    export let amount = 0;
    let displayAmount = false;

    const toggleDisplayAmount = () => {
        displayAmount = !displayAmount;
    }
</script>

<article class="single-expense">
    <div class="expense-info">
        <h2>
            {name}
            <button on:click = {toggleDisplayAmount} class="amount-btn"><i class="fas fa-caret-down" /></button>
        </h2>
        {#if displayAmount}
            <h4>amount: ${amount}</h4>
        {/if}
    </div>
    <div class="expense-buttons">
        <button class="expense-button edit-btn">
            <i class="fas fa-pen" />
        </button>
        <button class="expense-button delete-btn">
            <i class="fas fa-trash" />
        </button>
    </div>
</article>
