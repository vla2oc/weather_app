<template>
    <div class="city-selector">
      <label for="city-select" class="label">Select city:</label>
      <select
        id="city-select"
        v-model="city"
        @change="$emit('city-changed')"
        class="select"
      >
        <option v-for="city in cities" :key="city" :value="city">
          {{ city }}
        </option>
      </select>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      cities: {
        type: Array,
        required: true,
      },
      modelValue: {
        type: String,
        required: true,
      },
    },
    emits: ["update:modelValue", "city-changed"],
    computed: {
      city: {
        get() {
          return this.modelValue;
        },
        set(value) {
          this.$emit("update:modelValue", value);
        },
      },
    },
  };
  </script>
  
  <style scoped>
  .city-selector {
    margin-bottom: 20px;
  }
  
  .label {
    font-size: 1rem;
    margin-bottom: 5px;
    display: block;
    color: #555;
  }
  
  .select {
    padding: 10px;
    width: 100%;
    border: 1px solid #ccc;
    border-radius: 5px;
    font-size: 1rem;
  }
  </style>
  