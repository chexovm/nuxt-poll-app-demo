<template>
  <div>
    <div>Тип {{ id }}</div>
    <select
      @change="setChange($event.target.value)"
      class="type-component-select"
    >
      <option value="Silver">Silver</option>
      <option value="Gold">Gold</option>
      <option value="Platinum">Platinum</option>
    </select>
  </div>
</template>

<script>
export default {
  name: "Type",
  props: ["id"],
  data() {
    return {
      inputs: { optionId: this.$props.id, type: "Type", value: "" },
    };
  },
  methods: {
    setChange(value) {
      this.inputs.value = value;
      this.$emit("type-select-update", this.inputs);
    },
  },
};
</script>