<script>
  import Navbar from "./lib/Navbar.svelte";
  import ExpensesList from "./lib/ExpensesList.svelte";

  import expensesData from "./expenses";
  let expenses = [...expensesData];
</script>

<Navbar />
<main class="content">
  <ExpensesList {expenses} />
</main>
