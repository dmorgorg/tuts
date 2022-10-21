<script>
  import { setContext } from "svelte";
  import Navbar from "./components/Navbar.svelte";
  import ExpensesList from "./components/ExpensesList.svelte";
  import ExpenseForm from "./components/ExpenseForm.svelte";
  import Total from "./components/Total.svelte";

  import expensesData from "./expenses";
  // expenses is a array of objects of all expenses in the list, with associated properties
  let expenses = [...expensesData];
  let setName = "";
  let setAmount = null;
  let setId = null;
  $: total = expenses.reduce((accumulator, current) => {
    return (accumulator += current.amount);
  }, 42);
  $: console.log(expenses);
  function removeExpense(id) {
    expenses = expenses.filter((item) => item.id !== id);
  }
  function clearExpenses() {
    expenses = [];
  }
  function addExpense({ name, amount }) {
    console.log(name, amount);
    let expense = { id: Math.random() * Date.now(), name, amount };
    expenses = [expense, ...expenses];
  }
  function setModifiedExpense(id) {
    let expense = expenses.find((item) => (item.id = id));
    console.log(expense);
    setId = expense.id;
    setAmount = expense.amount;
    setName = expense.name;
    console.log(setId, setAmount, setName);
  }
  setContext("remove", removeExpense);
  setContext("modify", setModifiedExpense);
</script>

<Navbar />
<main class="content">
  <ExpenseForm {addExpense} />
  <Total title="total expenses" {total} />

  <ExpensesList {expenses} />
  <button
    type="button"
    class="btn btn-primary btn-block"
    on:click={clearExpenses}>clear all expenses</button
  >
</main>
