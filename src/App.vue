<script>
import { onMounted, computed, ref } from 'vue';

export default {
  name: 'NoteApp',
  setup() {
    const notes = ref([]);
    const newNote = ref('');

    const addNote = () => {
      if (newNote.value.trim() !== '') {
        notes.value.push(newNote.value);
        newNote.value = '';
      }
    };

    const removeNote = (index) => {
      notes.value.splice(index, 1);
    };

    const noteCount = computed(() => {
      return notes.value.length;
    });

    onMounted(() => {
      console.log('Note App mounted');
    });

    return {
      notes,
      newNote,
      addNote,
      removeNote,
      noteCount,
    };
  },
};
</script>

<template>
  <div class="note-app">
    <h1>Note App</h1>
    <form @submit.prevent="addNote">
      <input type="text" v-model="newNote" placeholder="Add a note...">
      <button class="add">Add</button>
    </form>
    <ul>
      <li v-for="(note, index) in notes" :key="index">
        {{ note }}
        <button class="remove" @click="removeNote(index)">Remove</button>
      </li>
    </ul>
    <p v-if="notes.length === 0">No notes yet. Add a note above.</p>
  </div>
</template>


<style>
.note-app {
  margin: 0 auto;
  padding: 20px;
  max-width: 600px;
  font-family: Arial, sans-serif;
}

h1 {
  text-align: center;
}

form {
  margin-bottom: 20px;
}

input[type="text"] {
  padding: 10px;
  font-size: 16px;
  border: none;
  border-radius: 4px;
  box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.1);
  width: 70%;
  margin-right: 10px;
}

button.add {
  padding: 10px;
  font-size: 16px;
  border: none;
  border-radius: 4px;
  background-color: #4CAF50;
  color: #fff;
  cursor: pointer;
}

button.add:hover {
  background-color: #3e8e41;
}

ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  font-size: 16px;
  border-bottom: 1px solid #ddd;
}

button.remove {
  padding: 5px;
  font-size: 12px;
  border: none;
  border-radius: 4px;
  background-color: #4CAF50;
  color: #fff;
  cursor: pointer;
}

button.remove:hover {
  background-color: #3e8e41;
}

p {
  text-align: center;
  font-size: 16px;
  color: #888;
}
</style>