<template>
  <div>
    <HeaderView :totalIncome="state.totalIncome" />
    <FormView @add-income="AddIncome" />
  </div>
</template>

<script>
import { reactive, computed } from "vue";
import HeaderView from "./components/HeaderView.vue";
import FormView from "./components/FormView.vue";

export default {
  setup() {
    const state = reactive({
      income: [],
      totalIncome: computed(() => {
        let temp = 0;

        if (state.income.length > 0) {
          for (let i = 0; i < state.income.length; i++) {
            temp += state.income[i].value;
          }
        }
        return temp;
      }),
    });

    function AddIncome(data) {
      let d = data.date.split("-")
      let newD = new Date(d[0], d[1], d[2])

      state.income = [...state.income, {
      id: Date.now(),
      desc: data.desc,
      value: data.value,
      date: newD.getTime()
      }]
    }
    return {
      state,
    };
  },
  components: {
    HeaderView,
    FormView,
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
