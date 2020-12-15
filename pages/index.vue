<template>
  <div class="container">
    <div class="navipanel">
      <img
        class="navipanel-item navipanel-img home"
        src="/home.png"
        alt="Иконка домой"
      />
      <img
        class="navipanel-item navipanel-img arrow"
        src="/arrow.jpg"
        alt="Стрелка вправо"
      />
      <span class="navipanel-item page">Опросы</span>
      <img
        class="navipanel-item navipanel-img arrow"
        src="/arrow.jpg"
        alt="Стрелка вправо"
      />
      <span class="navipanel-item action">Добавить опрос</span>
    </div>
    <div class="survey-menu-holder">
      <button
        v-for="tab in tabs"
        :key="tab.name"
        @click="selected = tab.component"
        :class="['survey-menu-btn', { active: selected === tab.component }]"
      >
        {{ tab.name }}
      </button>
    </div>
    <keep-alive>
      <component :is="selected"></component>
    </keep-alive>
  </div>
</template>

<script>
import Conditions from "../components/Conditions";
import Logic from "../components/Logic";
import Params from "../components/Params";
import Questions from "../components/Questions";
import Responders from "../components/Responders";

export default {
  data: function () {
    return {
      tabs: [
        { name: "Параметры", component: Params },
        { name: "Вопросы", component: Questions },
        { name: "Логика", component: Logic },
        { name: "Условия", component: Conditions },
        { name: "Респонденты", component: Responders },
      ],
      selected: "Responders",
    };
  },
  components: { Conditions, Logic, Params, Questions, Responders },
};
</script>

<style >
</style>
