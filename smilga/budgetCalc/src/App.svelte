<script>
  import Navbar from "./lib/Navbar.svelte";
  import ExpensesList from "./lib/ExpensesList.svelte";

  import expensesData from "./expenses";
  let expenses = [...expensesData];
  console.log(expenses);
  function removeExpense(id) {
    expenses = expenses.filter((item) => item.id !== id);
  }
  console.log(expenses);
</script>

<Navbar />
<main class="content">
  <ExpensesList {expenses} {removeExpense} />
</main>
