<template>
  <router-view/>

</template>

<script>

export default {
  name: "ExpenseTracker"
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
      text-align: left;
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
      justify-content: center;
      padding: 0.75rem 1rem;
      margin-bottom: 0.5rem;
      border-radius: 5px;
      background-color: #f9f9f9;
      border-left: 6px solid #ccc;
    }

    .transaction span {
      flex: 1;
    }
    .transaction span:first-child {
      text-align: left;
    }
    .transaction span:last-child {
      text-align: right;
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
