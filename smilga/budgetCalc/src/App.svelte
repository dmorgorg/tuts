<script>
  import { setContext } from "svelte";
  import Navbar from "./components/Navbar.svelte";
  import ExpensesList from "./components/ExpensesList.svelte";

  import expensesData from "./expenses";
  // expenses is a array of objects of all expenses in the list, with associated properties
  let expenses = [...expensesData];
  console.log(expenses)
  function removeExpense(id) {
    expenses = expenses.filter((item) => item.id !== id);
  }
  setContext("remove", removeExpense);
</script>

<Navbar />
<main class="content">
  <ExpensesList {expenses} />
</main>
