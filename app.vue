<script>
import { ref, computed } from "vue";

export default {
  setup() {
    const Income = ref(0); // Define as reactive ref
    const Expenses = ref(0);
    const AddIncome = ref(0); // Reactive input value
    const AddExpense = ref(0);

    const Balance = computed(() => {
      return Income.value - Expenses.value;
    });

    const updateIncome = () => {
      Income.value += parseFloat(AddIncome.value || 0); // Add input to Income
      AddIncome.value = 0; // Reset input
    };

    const updateExpense = () => {
      Expenses.value += parseFloat(AddExpense.value || 0); // Add input to Expenses
      AddExpense.value = 0; // Reset input
    };

    return {
      Income,
      Expenses,
      AddIncome,
      AddExpense,
      Balance, // Include Balance in the returned object
      updateIncome,
      updateExpense,
    };
  },
};
</script>

<template>
  <div class="app-container">
    <header class="header">
      <h1>Expense Tracker</h1>
    </header>

    <div class="balance-card">
      <h2>Balance</h2>
      <p class="balance-amount">{{ Balance }}</p>
    </div>

    <div class="info-cards">
      <div class="info-card income-card">
        <h3>Income</h3>
        <p>{{ Income }}</p>
      </div>
      <div class="info-card expense-card">
        <h3>Expenses</h3>
        <p>{{ Expenses }}</p>
      </div>
    </div>

    <section class="forms">
      <div class="form-group">
        <input
          type="number"
          v-model="AddIncome"
          placeholder="Add Income"
          class="input"
        />
        <button class="button" @click.prevent="updateIncome">Add Income</button>
      </div>
      <div class="form-group">
        <input
          type="number"
          v-model="AddExpense"
          placeholder="Add Expense"
          class="input"
        />
        <button class="button" @click.prevent="updateExpense">
          Add Expenses
        </button>
      </div>
    </section>
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;
}

.app-container {
  max-width: 500px;
  margin: 0 auto;
  padding: 20px;
  text-align: center;
  background: #f9f9f9;
  border-radius: 15px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
}

.header {
  margin-bottom: 20px;
}

.header h1 {
  font-size: 2rem;
  color: #333;
}

.balance-card {
  background: linear-gradient(145deg, #ffffff, #e6e6e6);
  border-radius: 10px;
  padding: 20px;
  margin-bottom: 20px;
  box-shadow: 20px 20px 60px #d1d1d1, -20px -20px 60px #ffffff;
}

.balance-card h2 {
  font-size: 1.5rem;
  color: #333;
}

.balance-amount {
  font-size: 2rem;
  color: #00a97f;
  font-weight: bold;
}

.info-cards {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}

.info-card {
  background: #fff;
  border-radius: 10px;
  padding: 15px;
  flex: 1;
  margin: 0 5px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
  text-align: center;
}

.income-card h3 {
  color: #00a97f;
}

.expense-card h3 {
  color: #e74c3c;
}

.form-group {
  margin-bottom: 15px;
}

.input {
  width: 80%;
  padding: 10px;
  margin-bottom: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
  font-size: 1rem;
  background: #f8f8f8;
  transition: 0.3s;
}

.input:focus {
  border-color: #00a97f;
  box-shadow: 0px 0px 5px rgba(0, 169, 127, 0.5);
  outline: none;
}

.button {
  width: 80%;
  padding: 10px;
  font-size: 1rem;
  color: #fff;
  background-color: #00a97f;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.3s;
}

.button:hover {
  background-color: #007f5f;
}
</style>
