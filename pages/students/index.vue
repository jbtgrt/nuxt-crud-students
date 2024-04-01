<template>
  <div class="container mt-5">
 
    <div class="card">
      <div class="card-header">
        <h4>Student Lists
          <NuxtLink to="/students/create" class="btn btn-primary float-end" >Add Student</NuxtLink>
        </h4>
      </div>
      <div class="card-body">
        <div v-if="isLoading">
          <Loading title="Loading" />
        </div>
        <div v-else>
          <table class="table table-striped table-bordered">
            <thead>
              <th>ID</th>
              <th>Name</th>
              <th>Course</th>
              <th>Email</th>
              <th>Phone</th>
              <th></th>
            </thead>
            <tbody>
              <tr v-for="(student, index) in this.students" :key="index">
                <td>{{ student.id }}</td>
                <td>{{ student.name }}</td>
                <td>{{ student.email }}</td>
                <td>{{ student.phone }}</td>
                <td>{{ student.created_at }}</td>
                <td>
                  <NuxtLink :to="`/students/${student.id}`" class="btn btn-success btn-sm mx-2">Edit</NuxtLink>
                  <button type="button" @click="deleteStudent($event, student.id)" class="btn btn-danger btn-sm mx-2">Delete</button>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from "axios";
  import { student_data } from "../../constants"

  export default {
    name: "student",
    data() {
      return {
        students: [],
        isLoading: false
      }
    },
    mounted() {
      this.getStudents();
    },
    methods: {
      getStudents() {
        this.isLoading = true;
        // The Code Below is Example to Get Students Data from backend
        // axios.get(`http://localhost:8000/api/students`).then(res => {
        //   this.students = res.data.students
        //   this.isLoading = false;
        // })
        
        // The Code Below is Example Get Students from constants
        this.students = student_data;
        this.isLoading = false;
      },

      deleteStudent(event, studentID) {
        
        if(confirm('Are you sure, you want to delete this data?')){
          event.target.innerText = 'Deleteing';
          // The Code Below is Example of Deleting Student to backend
          // axios.delete(`http://localhost:8000/api/students/${this.studentID}/delete`).then(res => {
          //   event.target.innerText = 'Delete';
          //   this.getStudents();
          // })
          
          // The Code Below is Example of Deleting Student to constants
          // Use filter to create a new array excluding the student with the specified ID
          const updatedStudentData = student_data.filter(student => student.id !== studentID);

          // Update the original student_data array with the filtered array
          student_data.splice(0, student_data.length, ...updatedStudentData);
          
          event.target.innerText = 'Delete';
          this.getStudents()
        }
      }
    }
  }
</script>