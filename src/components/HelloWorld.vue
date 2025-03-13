<template>
  <div id="page">
    <form @submit.prevent="add">
      <!-- <input type="hidden" v-model="id" /> -->
      <div class="frm-group">
        <label for="name">NAME:</label>
        <input type="text" v-model="name" required />
      </div>
      <div class="frm-group">
        <label for="age">AGE:</label>
        <input type="text" v-model="age" required />
      </div>
      <div class="frm-group">
        <label for="country">COUNTRY:</label>
        <input type="text" v-model="country" required />
      </div>
      <button type="submit" class="btn">SAVE</button>
    </form>

    <table>
      <thead>
        <tr>
          <th>S.no</th>
          <th>NAME</th>
          <th>AGE</th>
          <th>COUNTRY</th>
          <th>EDIT</th>
          <th>DELETE</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(person, index) in people" :key="index">
          <td>{{ index + 1 }}</td>
          <td>{{ person.name }}</td>
          <td>{{ person.age }}</td>
          <td>{{ person.country }}</td>
          <td><button @click="edit(index)">Edit</button></td>
          <td><button @click="del(index)">Delete</button></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// const id = ref(null);
const name = ref('');
const age = ref('');
const country = ref('');
const people = ref([]);
const editIndex = ref(-1);

const add = () => {
  
  if (!name.value || (!age.value) || !country.value) {
    alert("All fields are required.");
    return;
  }
  


  if (editIndex.value === -1) {
    people.value.push({ name: name.value, age: age.value, country: country.value });
  } else {
    people.value[editIndex.value] = { name: name.value, age: age.value, country: country.value };
    editIndex.value = -1;
  }

  name.value = '';
  age.value = '';
  country.value = '';
};

const edit = (index) => {
  name.value = people.value[index].name;
  age.value = people.value[index].age;
  country.value = people.value[index].country;
  editIndex.value = index;
};

const del = (index) => {
  people.value.splice(index, 1);
};
</script>



<style scoped>
  


body {
    padding: 6%;
    font-family: 'Arial', sans-serif;
    background-color: #ffffff;
    color: #333;
}


.frm-group {
    display: flex;
    align-items: center;
    justify-content: space-between; 
    width: 100%;
    max-width: 400px; 
    margin-bottom: 10px;
}

.frm-group input {
    padding: 8px;
  
    
    border: 1px solid #ccc;
    border-radius: 5px;
    font-size: 1rem;
    width: 68%; 
    box-sizing: border-box;
}


 button {
    padding: 10px 15px;
    background-color: #37c5f1;
    border: none;
    border-radius: 5px;
    color: white;
    font-size: 1rem;
    cursor: pointer;
    transition: background-color 0.3s ease;
}

form button:hover {
    background-color: #2a97c1;
}


table {
    width: 100%;
    max-width: 1000px;
    margin: 20px 0;
    border: 1px solid #959393;
    border-radius: 8px; 
    background-color: #fff;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    overflow: hidden; 
}

table th,
table td {
    border: 1px solid #ddd;
    padding: 12px 15px;
    text-align: center;
    font-size: 1rem;
}





table th {
    background-color: #33a1b1;
    color: white;
}
#page{
  
  padding: 40px 20px;
  
}
td{
  font-size: 1rem;
}



</style>
