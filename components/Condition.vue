<template>
  <div class="condition-component-div">
    <div class="condition-component-static-top">
      <div class="and-div" v-if="conditionArr.id > 1">И</div>
      <h4 class="condition-component-title">Условие {{ conditionArr.id }}</h4>
      <select
        class="condition-component-selector"
        @change="
          $emit('change-condition-type', [
            $event.target.value,
            conditionArr.id,
          ]);
          selected = $event.target.value;
          setButtonValue($event.target.value);
        "
        name="select-option"
      >
        <option value="" disabled selected>Выберите условие</option>
        <option value="Age">Возраст респондента</option>
        <option value="Type">Тип карты лояльности</option>
        <option value="Status">Статус карты лояльности</option>
      </select>
    </div>
    <keep-alive>
      <div class="option-wrapper">
        <component
          v-for="option in conditionArr.optionValues"
          :key="option.optionId"
          :is="selected"
          v-bind:id="option.optionId"
          v-on:age-form-update="optionUpdate"
          v-on:type-select-update="optionUpdate"
          v-on:status-select-update="optionUpdate"
        ></component>
      </div>
    </keep-alive>
    <button
      v-if="selected != ''"
      @click="$emit('add-option', [conditionArr.id, selected])"
      class="add-option condition-btn"
    >
      {{ `Добавить ${this.buttonValue}` }}
    </button>
    <button
      @click="$emit('delete-condition', conditionArr.id)"
      class="remove-condition condition-btn"
    >
      Удалить условие
    </button>
  </div>
</template>

<script>
import Age from "./conditions/Age";
import Type from "./conditions/Type";
import Status from "./conditions/Status";

export default {
  name: "Condition",
  data() {
    return {
      selected: "",
      buttonValue: "",
    };
  },
  components: {
    Age,
    Type,
    Status,
  },
  props: ["conditionArr"],
  methods: {
    setButtonValue(value) {
      switch (value) {
        case "Age":
          return (this.buttonValue = "диапазон");
          break;
        case "Type":
          return (this.buttonValue = "тип");
          break;
        case "Status":
          return (this.buttonValue = "статус");
          break;
        default:
          break;
      }
    },
    optionUpdate(obj) {
      this.$emit("optionsArr-update", [this.inputs, this.conditionArr.id]);
    },
  },
};
</script>