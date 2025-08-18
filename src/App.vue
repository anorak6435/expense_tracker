<template>
  <header>
    Income & Expense Tracker
  </header>

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

    <!-- Warnings -->
    <ul class="warnings">
      <li class="warning" v-for="(warning, key) in warnings" :key="key">
          <b>Warn:</b> {{warning}}
      </li>
    </ul>

    <!-- Add Transaction -->
    <div class="formular">
      <input type="text" placeholder="Description (e.g. Salary, Groceries)" ref="description" />
      <input type="number" placeholder="Amount (e.g. 100 or -50)" ref="amount" />
      <button @click="add_transaction">Add Transaction</button>
    </div>
    

    <!-- Transaction List -->
    <ul class="transaction-list" ref="transactions">
      <li v-for="(payment, key) in trans_abs" :key="key" class="transaction" :class="{expense: payment.amount < 0, income: payment.amount >= 0}">
        <span>{{payment.description}}</span>
        <span><span v-if="payment.is_income">+</span>
        <span v-else>-</span> €{{payment.abs}}</span>
      </li>
    </ul>
  </div>

</template>

<script>

export default {
  data() {
    return {
      warnings: [],
      transactions: [{description: "Salary", amount: 2500}, {description: "Groceries", amount: -150}, {description: "Movie tickets", amount: -40}, {description: "Book", amount: -25}],
    }
  },
  methods: {
    add_transaction() {
      console.log("New Transaction");
      let desc = this.$refs.description.value;
      let amnt = parseFloat(this.$refs.amount.value);

      let no_warnings = this.verify_transaction_form(desc, amnt);
      if (no_warnings) {
        this.transactions.push({"description": desc, "amount": amnt})
        // when succesfully added clear the contents of the form.
        this.$refs.description.value = "";
        this.$refs.amount.value = "";
      }
      console.log(desc, amnt);
      console.log(typeof amnt)
    },
    verify_transaction_form(desc, amnt) {
      this.warnings = [];
      if (desc == "") {
        this.warnings.push("Add a description");
      }
      if (amnt == "") {
        this.warnings.push("Add an amount for the transaction");
      }
      if (isNaN(amnt)) {
        this.warnings.push("Please enter a number for the amount");
      }
      return this.warnings.length == 0;
    }
  },
  computed: {
    trans_abs() {
      return this.transactions.map(transaction => {transaction.abs = Math.abs(transaction.amount); transaction.is_income = transaction.amount >= 0; return transaction})
    },
    income() {
      let incomes = this.trans_abs.filter(transaction => {return transaction.is_income});
      return incomes.reduce((accumulator, transaction) => accumulator + transaction.abs, 0);
    },
    expenses() {
      let expenses = this.trans_abs.filter(transaction => {return !transaction.is_income});
      return expenses.reduce((accumulator, transaction) => accumulator + transaction.abs, 0);
    },
    balance() {
      return this.income - this.expenses;
    }
  }
}
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}

* {
      box-sizing: border-box;
    }

    body {
      font-family: 'Segoe UI', sans-serif;
      background-color: #f4f6f8;
      margin: 0;
      padding: 0;
      color: #333;
    }

    header {
      background-color: #2c3e50;
      color: white;
      padding: 1.5rem;
      text-align: center;
      font-size: 1.8rem;
    }

    .container {
      max-width: 600px;
      margin: 2rem auto;
      background-color: #fff;
      padding: 2rem;
      border-radius: 8px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.05);
    }

    h2 {
      text-align: center;
      margin-bottom: 1rem;
    }

    .summary {
      display: flex;
      justify-content: space-between;
      background-color: #ecf0f1;
      padding: 1rem;
      border-radius: 6px;
      margin-bottom: 2rem;
    }

    .summary div {
      text-align: center;
    }

    .summary h3 {
      margin: 0 0 0.5rem;
    }

    .formular {
      display: flex;
      flex-direction: column;
      margin-bottom: 2rem;
    }

    .formular input, .formular button {
      padding: 0.75rem;
      margin-bottom: 1rem;
      border: 1px solid #ccc;
      border-radius: 6px;
      font-size: 1rem;
    }

    .formular button {
      background-color: #27ae60;
      color: white;
      border: none;
      cursor: pointer;
      transition: background-color 0.3s;
    }

    .formular button:hover {
      background-color: #1e8449;
    }

    .warnings {
      list-style: none;
      color: #c0392b;
    }

    .transaction-list {
      list-style: none;
      padding: 0;
    }

    .transaction {
      display: flex;
      justify-content: space-between;
      padding: 0.75rem 1rem;
      margin-bottom: 0.5rem;
      border-radius: 5px;
      background-color: #f9f9f9;
      border-left: 6px solid #ccc;
    }

    .transaction.income {
      border-color: #27ae60;
      color: #27ae60;
    }

    .transaction.expense {
      border-color: #c0392b;
      color: #c0392b;
    }

    @media (max-width: 600px) {
      .summary {
        flex-direction: column;
        gap: 1rem;
      }
    }
</style>
