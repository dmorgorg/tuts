<script>
  import { setContext } from "svelte";
  import Navbar from "./components/Navbar.svelte";
  import ExpensesList from "./components/ExpensesList.svelte";
  import ExpenseForm from "./components/ExpenseForm.svelte";
  import Total from "./components/Total.svelte";

  import expensesData from "./expenses";
  // expenses is a array of objects of all expenses in the list, with associated properties
  let expenses = [...expensesData];
  // let expenses = [];
  // editing variables
  let setName = "";
  let setAmount = null;
  let setId = null;
  $: isEditing = setId ? true : false;
  $: total = expenses.reduce((accumulator, current) => {
    return (accumulator += current.amount);
  }, 0);

  function removeExpense(id) {
    expenses = expenses.filter((item) => item.id !== id);
  }

  function clearExpenses() {
    expenses = [];
  }

  function addExpense({ name, amount }) {
    let expense = { id: Math.random() * Date.now(), name, amount };
    expenses = [expense, ...expenses];
  }

  function setModifiedExpense(id) {
    let expense = expenses.find((item) => (item.id = id));
    setId = expense.id;
    setAmount = expense.amount;
    setName = expense.name;
  }

  function editExpense({ name, amount }) {
    expenses = expenses.map((item) => {
      return item.id === setId ? { ...item, name, amount } : item;
    });
    setId = null;
    setAmount = null;
    setName = "";
  }
  setContext("remove", removeExpense);
  setContext("modify", setModifiedExpense);
</script>

<Navbar />
<main class="content">
  <ExpenseForm
    {addExpense}
    name={setName}
    amount={setAmount}
    {isEditing}
    {editExpense}
  />
  <Total title="total expenses" {total} />

  <ExpensesList {expenses} />
  <button
    type="button"
    class="btn btn-primary btn-block"
    on:click={clearExpenses}>clear all expenses</button
  >
</main>
