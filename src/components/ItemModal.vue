<template>
    <div class="modal">
      <div class="modal-content">
        <span class="close" @click="$emit('close')">&times;</span>
        <h2>{{ isEdit ? 'Edit' : 'Add' }} Item</h2>
        <form @submit.prevent="onSubmit">
          <div>
            <label for="name">Name:</label>
            <input type="text" v-model="localItem.name" required>
          </div>
          <div>
            <label for="age">Age:</label>
            <input type="number" v-model="localItem.age" required>
          </div>
          <div>
            <label for="gender">Gender:</label>
            <select v-model="localItem.gender" required>
              <option>Male</option>
              <option>Female</option>
              <option>Other</option>
            </select>
          </div>
          <div>
            <label for="mobile">Mobile:</label>
            <input type="text" v-model="localItem.mobile" required>
          </div>
          <button type="submit">{{ isEdit ? 'Update' : 'Add' }}</button>
        </form>
      </div>
    </div>
  </template>
  
  <script>
  import { ref, watch } from 'vue';
  
  export default {
    name: 'ItemModal',
    props: {
      item: Object,
      isEdit: Boolean,
    },
    setup(props, { emit }) {
      const localItem = ref({ ...props.item });
  
      watch(props.item, (newVal) => {
        localItem.value = { ...newVal };
      });
  
      const onSubmit = () => {
        emit('save', localItem.value);
      };
  
      return { localItem, onSubmit };
    },
  };
  </script>
  
  <style scoped>
  .modal {
    display: flex;
    justify-content: center;
    align-items: center;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
  }
  
  .modal-content {
    background-color: #fff;
    padding: 20px;
    border-radius: 5px;
    width: 300px;
    text-align: center;
  }
  
  .close {
    float: right;
    font-size: 20px;
    cursor: pointer;
  }
  </style>
  