<template>
  <div>
    <h1>CRUD Operations</h1>
    <button @click="openAddModal">Add</button>
    <ItemTable :items="items" @edit="openEditModal" @delete="deleteItem" />
    <ItemModal
      v-if="showModal"
      :item="currentItem"
      :isEdit="isEdit"
      @save="saveItem"
      @close="closeModal"
    />
  </div>
</template>

<script>
import { ref } from 'vue';
import ItemTable from './ItemTable.vue';
import ItemModal from './ItemModal.vue';

export default {
  name: 'CrudTable',
  components: { ItemTable, ItemModal },
  setup() {
    const items = ref([
      { name: 'John Doe', age: 30, gender: 'Male', mobile: '123-456-7890' },
      // Add more initial items if needed
    ]);
    const showModal = ref(false);
    const isEdit = ref(false);
    const currentItem = ref({ name: '', age: '', gender: '', mobile: '' });
    const currentIndex = ref(null);

    const openAddModal = () => {
      isEdit.value = false;
      currentItem.value = { name: '', age: '', gender: '', mobile: '' };
      showModal.value = true;
    };

    const openEditModal = (index) => {
      isEdit.value = true;
      currentIndex.value = index;
      currentItem.value = { ...items.value[index] };
      showModal.value = true;
    };

    const closeModal = () => {
      showModal.value = false;
    };

    const saveItem = (item) => {
      if (isEdit.value) {
        items.value[currentIndex.value] = { ...item };
      } else {
        items.value.push({ ...item });
      }
      closeModal();
    };

    const deleteItem = (index) => {
      items.value.splice(index, 1);
    };

    return {
      items,
      showModal,
      isEdit,
      currentItem,
      openAddModal,
      openEditModal,
      closeModal,
      saveItem,
      deleteItem,
    };
  },
};
</script>
