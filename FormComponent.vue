<template>
  <form @submit.prevent="handleSubmit">
    <div v-for="field in fields" :key="field.name">
      <label :for="field.name">{{ field.label }}</label>
      <input
        :type="field.type"
        :id="field.name"
        v-model="formData[field.name]"
        :required="field.required"
      />
    </div>
    <button type="submit">Submit</button>
  </form>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
  fields: {
    type: Array,
    required: true,
    validator: (value) => {
      return value.every(field => 
        field.name && field.label && field.type
      );
    }
  },
  onSubmit: {
    type: Function,
    required: true
  }
});

const formData = ref({});

const handleSubmit = () => {
  props.onSubmit(formData.value);
};
</script>

<style scoped>
form {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

label {
  display: block;
  margin-bottom: 5px;
}

input {
  width: 100%;
  padding: 8px;
  margin-bottom: 15px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  background-color: #42b983;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #3aa876;
}
</style>
