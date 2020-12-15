<template>
  <div>
    <div>Статус {{ id }}</div>
    <select
      @change="setChange($event.target.value)"
      class="status-component-select"
    >
      <option value="Active">Active</option>
      <option value="Inactive">Gold</option>
    </select>
  </div>
</template>

<script>
export default {
  name: "Status",
  props: ["id"],
  data() {
    return {
      inputs: { optionId: this.$props.id, type: "Status", value: "" },
    };
  },
  methods: {
    setChange(value) {
      this.inputs.value = value;
      this.$emit("status-select-update", this.inputs);
    },
  },
};
</script>