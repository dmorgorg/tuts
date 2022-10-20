<script>
  import { setContext } from "svelte";
  import Navbar from "./components/Navbar.svelte";
  import ExpensesList from "./components/ExpensesList.svelte";
  import ExpenseForm from "./components/ExpenseForm.svelte";
  import Total from "./components/Total.svelte";

  import expensesData from "./expenses";
  // expenses is a array of objects of all expenses in the list, with associated properties
  let expenses = [...expensesData];
  $: total = expenses.reduce((accumulator, current) => {
    return accumulator += current.amount;
  },42);
  console.log(expenses);
  function removeExpense(id) {
    expenses = expenses.filter((item) => item.id !== id);
  }
  function clearExpenses() {
    expenses = [];
  }
  setContext("remove", removeExpense);
</script>

<Navbar />
<main class="content">
  <ExpenseForm />
  <Total title="total expenses" {total} />
  
  <ExpensesList {expenses} />
  <button
    type="button"
    class="btn btn-primary btn-block"
    on:click={clearExpenses}>clear all expenses</button
  >
</main>
