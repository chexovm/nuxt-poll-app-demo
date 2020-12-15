<template>
  <div class="condition-wrapper">
    <h3 class="condition-title">Добавить опрос</h3>
    <div
      class="condition-component-outerdiv"
      v-for="condition in conditionArr"
      :key="condition.id"
      v-bind:id="condition.id"
    >
      <Condition
        v-bind:conditionArr="condition"
        v-on:add-option="addOption"
        v-on:change-condition-type="changeConditionType"
        v-on:age-form-update="optionUpdate"
        v-on:delete-condition="deleteCondition"
      />
    </div>
    <button class="add-condition condition-btn" @click="addCondition">
      Нажмите сюда, чтобы добавить новое условие выборки. Все условия
      связываются между собой логическим "И".
    </button>
    <div class="final-submit-buttons">
      <button class="condition-btn test-button" @click="submitPoll">
        Протестировать опрос</button
      ><button class="condition-btn submit-button" @click="submitPoll">
        Отправка запроса
      </button>
    </div>
  </div>
</template>

<script>
import Condition from "./Condition";

export default {
  name: "Responders",
  components: { Condition },
  data() {
    return {
      conditionArr: [
        {
          id: 1,
          type: "",
          optionValues: [{ optionId: 1, type: "", values: [] }],
        },
      ],
    };
  },
  methods: {
    deleteCondition(id) {
      this.conditionArr = this.conditionArr.filter(
        (condition) => condition.id !== id
      );
    },
    addCondition() {
      let lastEl = this.conditionArr.length - 1;
      if (this.conditionArr.length < 1) {
        return (this.conditionArr = [
          {
            id: 1,
            type: "",
            optionValues: [{ optionId: 1, type: "", values: [] }],
          },
        ]);
      }
      return this.conditionArr.push({
        id: this.conditionArr[lastEl].id + 1,
        type: "",
        optionValues: [{ optionId: 1, type: "", values: [] }],
      });
    },
    changeConditionType([type, id]) {
      return this.conditionArr.map((el) => {
        if (el.id === id) {
          el.type = type;
          el.optionValues = [{ optionId: 1, type: "", values: [] }];
        }
      });
    },
    optionUpdate([object, conditionId]) {
      return this.conditionArr.map((el) => {
        if (el.id === conditionId) {
          return el.optionValues.map((option) => {
            if (option.id === object.id) {
              return (option = object);
            }
          });
        }
      });
    },
    addOption([conditionId, optionType]) {
      return this.conditionArr.map((el) => {
        if (el.id === conditionId) {
          let lastOption = el.optionValues.length - 1;
          let newOptionId = el.optionValues[lastOption].optionId + 1;
          el.optionValues.push({
            optionId: newOptionId,
            type: optionType,
            values: [],
          });
        }
      });
    },

    async submitPoll() {
      let { conditionArr } = this;
      const requestOptions = {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ conditionArr }),
      };
      const response = await fetch(
        "https://jsonplaceholder.typicode.com/posts",
        requestOptions
      );
      const data = await response.json();
      console.log(data);
    },
  },
};
</script>