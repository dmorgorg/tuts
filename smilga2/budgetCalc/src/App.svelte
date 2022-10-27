<script>
  import { setContext, onMount, afterUpdate } from "svelte";

  import Navbar from "./components/Navbar.svelte";
  import ExpensesList from "./components/ExpensesList.svelte";
  import ExpenseForm from "./components/ExpenseForm.svelte";
  import Total from "./components/Total.svelte";

  // import expensesData from "./expenses";
  // expenses is a array of objects of all expenses in the list, with associated properties
  let expenses = [];
  // let expenses = [];
  // editing variables
  let setName = "";
  let setAmount = null;
  let setId = null;
  let isFormOpen = false;

  $: isEditing = setId ? true : false;
  $: total = expenses.reduce((accumulator, current) => {
    return (accumulator += current.amount);
  }, 0);

  function showForm() {
    isFormOpen = true;
  }
  function hideForm() {
    isFormOpen = false;
    setName = "";
    setAmount = null;
    setId = null;
  }

  function removeExpense(id) {
    expenses = expenses.filter((item) => item.id !== id);
    // setLocalStorage();
  }

  function clearExpenses() {
    expenses = [];
    // setLocalStorage();
  }

  function addExpense({ name, amount }) {
    let expense = { id: Math.random() * Date.now(), name, amount };
    expenses = [expense, ...expenses];
    // setLocalStorage();
  }

  function setModifiedExpense(id) {
    showForm();
    let expense = expenses.find((item) => (item.id = id));
    setId = expense.id;
    setAmount = expense.amount;
    setName = expense.name;
    // setLocalStorage();
  }

  function editExpense({ name, amount }) {
    expenses = expenses.map((item) => {
      return item.id === setId ? { ...item, name, amount } : item;
    });
    setId = null;
    setAmount = null;
    setName = "";
    // setLocalStorage();
  }
  setContext("remove", removeExpense);
  setContext("modify", setModifiedExpense);

  function setLocalStorage() {
    localStorage.setItem("expenses", JSON.stringify(expenses));
  }
  onMount(() => {
    // console.log(localStorage.getItem("expenses"))
    expenses = localStorage.getItem("expenses")
      ? JSON.parse(localStorage.getItem("expenses"))
      : [];
  });
  afterUpdate(() => {
    setLocalStorage();
  });
</script>

<Navbar {showForm} />
<main class="content">
  {#if isFormOpen}
    <ExpenseForm
      {addExpense}
      name={setName}
      amount={setAmount}
      {isEditing}
      {editExpense}
      {hideForm}
    />
  {/if}
  <Total title="total expenses" {total} />

  <ExpensesList {expenses} />
  <button
    type="button"
    class="btn btn-primary btn-block"
    on:click={clearExpenses}>clear all expenses</button
  >
</main>
