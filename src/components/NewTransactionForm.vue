<template>
  <!-- Add Transaction -->
  <div class="formular">
    <input
      type="text"
      placeholder="Description (e.g. Salary, Groceries)"
      ref="description"
    />
    <input type="number" placeholder="Amount (e.g. 100 or -50)" ref="amount" />
    <input type="text" placeholder="From where" ref="from" />
    <input type="text" placeholder="To where" ref="to" />
    <label for="when">Transaction date:</label>
    <input type="date" id="when" name="when" placeholder="" ref="when" />
    <button @click="add_transaction">Add Transaction</button>
  </div>
  <!-- Warnings -->
  <ul class="warnings">
    <li class="warning" v-for="(warning, key) in warnings" :key="key">
      <b>Warn:</b> {{ warning }}
    </li>
  </ul>
</template>

<script>
export default {
  name: "NewTransactionForm",
  data() {
    return {
      warnings: [],
    };
  },
  methods: {
    add_transaction() {
      console.log("New Transaction");
      let desc = this.$refs.description.value;
      let amnt = parseFloat(this.$refs.amount.value);
      let when = this.$refs.when.value;
      let from = this.$refs.from.value;
      let to = this.$refs.to.value;

      let no_warnings = this.verify_transaction_form(
        desc,
        amnt,
        when,
        from,
        to
      );
      if (no_warnings) {
        // this.transactions.push(
        this.$emit("pushTransaction", {
          description: desc,
          amount: amnt,
          when: when,
          from: from,
          to: to,
        });
        // when succesfully added clear the contents of the form.
        this.$refs.description.value = "";
        this.$refs.amount.value = "";
        this.$refs.when.value = "";
        this.$refs.from.value = "";
        this.$refs.to.value = "";
      }
    },

    verify_transaction_form(desc, amnt, when, from, to) {
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
      if (when == "") {
        this.warnings.push("Please add the date of this transaction.");
      }
      if (from == "") {
        this.warnings.push("Add a from description");
      }
      if (to == "") {
        this.warnings.push("Add a to description");
      }
      return this.warnings.length == 0;
    },
  },
};
</script>

<style>
</style>