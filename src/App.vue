<template>
  <div>
    <h1>Daftar Mahasiswa</h1>
    <div v-if="students.length === 0">Belum ada data mahasiswa</div>
    <ul v-else>
      <li v-for="(student, index) in students" :key="index" class="student-item">
        <div class="student-info">
          <strong>{{ student.name }}</strong> - {{ student.major }}
        </div>
        <div class="student-actions">
          <button @click="editStudent(index)">Edit</button>
          <button @click="deleteStudent(index)">Delete</button>
        </div>
      </li>
    </ul>
    <div v-if="editingIndex !== null" class="edit-form">
      <h2>Edit Mahasiswa</h2>
      <input type="text" v-model="editedStudent.name" placeholder="Nama">
      <input type="text" v-model="editedStudent.major" placeholder="Jurusan">
      <button @click="updateStudent">Update</button>
    </div>
    <div class="add-form">
      <h2>Tambah Mahasiswa Baru</h2>
      <input type="text" v-model="newStudent.name" placeholder="Nama">
      <input type="text" v-model="newStudent.major" placeholder="Jurusan">
      <button @click="addStudent">Tambah</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      students: [],
      newStudent: {
        name: '',
        major: ''
      },
      editingIndex: null,
      editedStudent: {
        name: '',
        major: ''
      }
    };
  },
  methods: {
    addStudent() {
      if (this.newStudent.name.trim() !== '' && this.newStudent.major.trim() !== '') {
        this.students.push({ ...this.newStudent });
        this.newStudent.name = '';
        this.newStudent.major = '';
      }
    },
    editStudent(index) {
      this.editingIndex = index;
      this.editedStudent = { ...this.students[index] };
    },
    updateStudent() {
      if (this.editedStudent.name.trim() !== '' && this.editedStudent.major.trim() !== '') {
        this.students[this.editingIndex] = { ...this.editedStudent };
        this.editingIndex = null;
        this.editedStudent = { name: '', major: '' };
      }
    },
    deleteStudent(index) {
      this.students.splice(index, 1);
    }
  }
};
</script>

<style scoped>
/* CSS untuk mengatur tampilan komponen */
ul {
  list-style-type: none;
  padding: 0;
}
.student-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
}
.student-info {
  flex: 1;
}
.student-actions {
  margin-left: 10px;
}
.edit-form,
.add-form {
  margin-top: 20px;
}
input {
  margin-bottom: 10px;
}
button {
  padding: 5px 10px;
  margin-right: 5px;
}
</style>
