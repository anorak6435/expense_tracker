<template>
  <header>
    Income & Expense Tracker
  </header>
  <nav>
    <RouterLink to="/">Transactions</RouterLink>
  </nav>

  <div class="container">
    <h2>Track Your Finances</h2>

    <!-- Summary -->
    <div class="summary">
      <div>
        <h3>Balance</h3>
        <p>€{{balance}}</p>
      </div>
      <div>
        <h3>Income</h3>
        <p>€{{income}}</p>
      </div>
      <div>
        <h3>Expenses</h3>
        <p>€{{expenses}}</p>
      </div>
    </div>

    <NewTransactionForm @push-transaction="pushTransaction"/>
    

    <!-- Transaction List -->
    <ul class="transaction-list" ref="transactions">
      <!-- Header for the transactions list -->
      <li class="transaction">
        <span>Description</span>
        <span>Date</span>
        <span>From</span>
        <span>To</span>
        <span>Amount</span>
      </li>
      <TransactionComp v-for="(payment, key) in transaction_absolutes" :key="key" v-bind="payment" />
    </ul>
  </div>
</template>

<script>
import TransactionComp from '@/components/TransactionComp.vue';
import NewTransactionForm from '@/components/NewTransactionForm.vue';
export default {
    name: "HomeView",
    data() {
    return {
      transactions: [{description: "Salary", amount: 2500, when: "2025-07-01", from: "Work", to: "Checking"}, {description: "Groceries", amount: -150, when: "2025-07-15", from: "Checking", to: "Market"}, {description: "Movie tickets", amount: -40, when: "2025-07-20", from: "Checking", to: "Cinema"}, {description: "Book", amount: -25, when: "2025-08-05", from: "Checking", to: "Market"}],
    }
  },
  components: {
    TransactionComp,
    NewTransactionForm
  },
  methods: {
    pushTransaction(transaction) {
      this.transactions.push(transaction);
    }
  },
  
  computed: {
    transaction_absolutes() {
      return this.transactions.map(transaction => {transaction.absolute = Math.abs(transaction.amount); transaction.is_income = transaction.amount >= 0; return transaction})
    },
    income() {
      let incomes = this.transaction_absolutes.filter(transaction => {return transaction.is_income});
      return incomes.reduce((accumulator, transaction) => accumulator + transaction.absolute, 0);
    },
    expenses() {
      let expenses = this.transaction_absolutes.filter(transaction => {return !transaction.is_income});
      return expenses.reduce((accumulator, transaction) => accumulator + transaction.absolute, 0);
    },
    balance() {
      return this.income - this.expenses;
    },
    
  }
}
</script>

<style>

</style>