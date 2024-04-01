<template>
  <div class="mt-5 container">
   
    <div class="card">
      <div class="card-header">
        <h4>Add Student
          <NuxtLink to="/students" class="btn btn-danger float-end">Back</NuxtLink>
        </h4>
      </div>
      <div class="card-body">

        <div v-if="isLoading">
          <Loading :title="isLoadingTitle" />
        </div>
        <div v-else>
          <form @submit.prevent="saveStudent">
            <div class="mb-3">
              <label for="name">Name</label>
              <input type="text" id="name" class="form-control" v-model="student.name" />
              <span class="text-danger" v-if="this.errorList.name">{{ this.errorList.name[0] }}</span>
            </div>
            <div class="mb-3">
              <label for="course">Course</label>
              <input type="text" id="course" class="form-control" v-model="student.course" />
              <span class="text-danger" v-if="this.errorList.course">{{ this.errorList.course[0] }}</span>
            </div>
            <div class="mb-3">
              <label for="email">Email</label>
              <input type="text" id="email" class="form-control"  v-model="student.email"  />
              <span class="text-danger" v-if="this.errorList.email">{{ this.errorList.email[0] }}</span>
            </div>
            <div class="mb-3">
              <label for="phone">Phone</label>
              <input type="text" id="phone" class="form-control"  v-model="student.phone" />
              <span class="text-danger" v-if="this.errorList.phone">{{ this.errorList.phone[0] }}</span>
            </div>
            <div class="mb-3">
              <button type="submit" class="btn btn-primary">Save</button>
            </div>
          </form>
        </div>
        
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { student_data } from "../../constants"

export default {
  name: "studentCreate",
  data() {
    return {
      student: {
        name: '',
        course: '',
        email: '',
        phone: ''
      },
      isLoading: false,
      isLoadingTitle: 'Loading',
      errorList: {}
    }
  },
  methods: {
    saveStudent(){
      this.isLoading = true;
      this.isLoadingTitle = "Saving";

      var myThis = this;

      // The Code Below is Example Save Student to backend
      // axios.post(`http://localhost:8000/api/students`, this.student).then(res => {
      //   console.log(res, 'res');
      //   alert(res.data.message);

      //   this.student.name = '';
      //   this.student.course = '';
      //   this.student.email = '';
      //   this.student.phone = '';

      //   this.isLoading = false;
      //   this.isLoadingTitle = "Loading";

      //   this.errorList = {}
      // })
      // .catch(error => {
      //   console.log(error);

      //   if(error.response){
      //     if(error.response.status == 422){
      //       myThis.errorList = error.response.data.errors;
      //     }
      //   }

      //   myThis.isLoading = false;
      // })
      
      // The Code Below is Example of Saving Student to constants
      // Generate a new ID for the student (you may use a more robust method in a real application)
      const newStudentID = student_data.length + 1;

      // Add the new student to the array with the generated ID
      const created_at = new Date().toLocaleDateString(); // Get the current date as a string
      const studentWithID = {
        id: newStudentID,
        created_at,
        ...this.student,
      };

      student_data.push(studentWithID);

      alert('Saved Successfully!');

      this.student.name = '';
      this.student.course = '';
      this.student.email = '';
      this.student.phone = '';

      this.isLoading = false;
      this.isLoadingTitle = "Loading";
    }
  }
}
</script>