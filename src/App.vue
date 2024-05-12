<template>
  <div :class="{ 'dark-mode': isDarkMode }" class="container">
    <div class="content">
      <h1>Masukkan Data</h1>
      <table>
        <thead>
          <tr>
            <th>Nama dan Umur</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(person, index) in people" :key="index">
            <td><input v-model="person.data" placeholder="Nama dan Umur" class="input-field" /></td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="content">
      <h1>Data yang Telah Dimasukkan</h1>
      <table>
        <thead>
          <tr>
            <th>Nama</th>
            <th>Umur</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(person, index) in submittedPeople" :key="index">
            <td>{{ person.name }}</td>
            <td>{{ person.age }}</td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="controls">
      <button @click="submitData">Submit</button>
      <button @click="toggleDarkMode">{{ isDarkMode ? 'Light Mode' : 'Dark Mode' }}</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      people: [{ data: '' }],
      submittedPeople: [],
      isDarkMode: false
    };
  },
  methods: {
    submitData() {
      this.people.forEach(person => {
        if (person.data.trim() !== '') {
          const [name, age] = person.data.split(' ');
          this.submittedPeople.push({ name, age });
          person.data = ''; // Reset input setelah submit
        }
      });
    },
    toggleDarkMode() {
      this.isDarkMode = !this.isDarkMode;
    }
  }
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #f2f2f2; /* Latar belakang cerah */
  padding: 20px;
  border-radius: 10px;
}

.content {
  margin-bottom: 20px;
}

h1 {
  margin-bottom: 10px;
  color: #333; /* Warna teks gelap */
  font-size: 24px; /* Ukuran teks */
}

.dark-mode h1 {
  color: #fff; /* Warna teks pada mode gelap */
}

table {
  width: 100%;
  border-collapse: collapse;
}

th, td, .input-field, button {
  color: #333; /* Warna teks gelap */
}

.dark-mode th, .dark-mode td, .dark-mode .input-field, .dark-mode button {
  color: #fff; /* Warna teks pada mode gelap */
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
}

.dark-mode th, .dark-mode td {
  color: #fff; /* Warna teks pada mode gelap */
}

.dark-mode {
  background-color: #333;
}

.controls {
  margin-top: 20px;
}

.input-field {
  width: calc(100% - 20px); /* Lebar input mengikuti sel tabel dengan padding */
  padding: 10px;
  font-size: 16px; /* Ukuran teks */
  color: #333; /* Warna teks gelap */
  background-color: #fff; /* Warna latar belakang putih */
  border: 1px solid #ccc; /* Garis border */
  border-radius: 4px; /* Sudut border */
}

.dark-mode .input-field {
  background-color: #444; /* Warna latar belakang input pada dark mode */
  color: #fff; /* Warna teks input pada dark mode */
  border-color: #666; /* Warna border input pada dark mode */
}

button {
  padding: 10px 20px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}

.dark-mode button {
  background-color: #555;
  border-color: #777;
}

.dark-mode button:hover {
  background-color: #666;
}
</style>