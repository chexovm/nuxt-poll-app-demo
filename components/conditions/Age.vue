<template>
  <div class="age-component-range">
    <div class="or-div" v-if="id > 1">или</div>
    <div class="age-component-range">
      <div class="age-num">Диапазон {{ id }}</div>
      <form class="age-component-form" action="submit">
        <div>
          от:
          <input @change="setChange($event.target.value, 0)" type="text" />
        </div>
        <div>
          до:
          <input @change="setChange($event.target.value, 1)" type="text" />
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "Age",
  props: ["id"],
  data() {
    return {
      inputs: { optionId: this.$props.id, type: "Age", value: [] },
    };
  },
  methods: {
    setChange(value, index) {
      this.inputs.value[index] = value;
      this.$emit("age-form-update", this.inputs);
    },
  },
};
</script>