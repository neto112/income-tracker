<template>
  <div>
    <HeaderView :totalIncome="state.totalIncome" />
    <FormView  :state="state" @add-income="AddIncome" />
    <IncomeList :state="state" @remove-item="removeItem" />
  </div>
</template>

<script>
import { reactive, computed } from "vue";
import HeaderView from "./components/HeaderView.vue";
import FormView from "./components/FormView.vue";
import IncomeList from "./components/IncomeList.vue"

export default {
  setup() {
    const state = reactive({
      income: [],
      sortedIncome: computed(() => {
        let temp = [];
        
        temp = state.income.sort((a, b) => {
          return b.date - a.date;
        });
        return temp;
      }),

      totalIncome: computed(() => {
        let temp = 0;
        if (state.income.length > 0) {
          for (let i = 0; i < state.income.length; i++) {
            temp += state.income[i].value;
          }
        return temp;
        } else {
          return 0;
        }
      }),
    });

    function AddIncome(data) {
      let d = data.date.split("-")
      console.log("d >>>", d);
      console.log(new Date());
      let newD = new Date(d[0], d[1] -1, d[2])
      console.log("newD >>>", newD);

      state.income = [...state.income, {
      id: Date.now(),
      desc: data.desc,
      value: parseInt(data.value),
      date: newD.getTime()
      }]
      // console.log(state.income);
    }
    return {
      state,
      AddIncome
    };
  },
  components: {
    HeaderView,
    FormView,
    IncomeList
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Fira Sans", sans-serif;
}

body {
  background: #eee;
}
</style>
