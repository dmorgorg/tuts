<script>
  import Navbar from "./lib/Navbar.svelte";
  import ExpenseList from "./lib/ExpensesList.svelte";

  import expensesData from "./expenses";
  let expenses = [...expensesData];
</script>

<Navbar />
<main class="content">
  <ExpenseList />
</main>
