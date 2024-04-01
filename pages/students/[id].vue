<template>
  <div class="mt-5 container">
   
    <div class="card">
      <div class="card-header">
        <h4>Edit Student
          <NuxtLink to="/students" class="btn btn-danger float-end">Back</NuxtLink>
        </h4>
      </div>
      <div class="card-body">

        <div v-if="isLoading">
          <Loading :title="isLoadingTitle" />
        </div>
        <div v-else>
          <form @submit.prevent="updateStudent">
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
              <button type="submit" class="btn btn-primary">Update</button>
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
  name: "studentEdit",
  data() {
    return {
      studentID: '',
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
  mounted() {
    this.studentID = this.$route.params.id;
    // alert(this.studentID)

    this.getStudent(this.studentID);
  },
  methods: {
    getStudent(studentID) {

      this.isLoading = true;

      // The Code Below is Example of getting Student Data By his ID from backend
      // axios.get(`http://localhost:8000/api/students/${studentID}/edit`).then(res => {
      //   console.log(res);
      //   this.student = res.data.student;
      //   this.isLoading = false;
      // });
      
      // The Code Below is Example of getting Student Data By his ID from constants
      this.student = student_data.find(student => student.id == studentID);
      this.isLoading = false;
    },

    updateStudent(){
      this.isLoading = true;
      this.isLoadingTitle = "Updating";

      var myThis = this;
      
      // The code below is example of updating student data from backed
      axios.put(`http://localhost:8000/api/students/${this.studentID}/edit`, this.student).then(res => {
        console.log(res, 'res');
        alert(res.data.message);

        this.isLoading = false;
        this.isLoadingTitle = "Loading";

        this.errorList = {}
      })
      .catch(error => {
        // console.log(error);

        if(error.response){

          if(error.response.status == 422){
            myThis.errorList = error.response.data.errors;
          }
        }

        myThis.isLoading = false
      })

    }
  }
}
</script>