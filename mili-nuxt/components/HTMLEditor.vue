<template>
  <div class="golang123-editor">
    <Input
      v-model="inputValue"
      @on-change="onChange"
      type="textarea"
      :rows="40"
    ></Input>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      required: true,
    },
    user: {
      type: Object,
    },
  },
  data() {
    return {
      inputValue: this.value || "",
    };
  },
  methods: {
    onSave() {
      this.$emit("save");
    },
    onChange() {
      this.$emit("change", this.inputValue);
    },
  },
  head() {
    return {};
  },
  mounted() {
    console.log(11111, this.value);
  },
};
</script>
