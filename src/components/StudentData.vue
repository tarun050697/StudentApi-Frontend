<template>
  <div v-if="listStudent">
    <div class="container">
      <div class="row height d-flex justify-content-center align-items-center">
        <div class="col-md-5">
          <div class="search">
            <i class="fa fa-search"></i>
            <input
              type="text"
              class="form-control"
              placeholder="Type Something"
              v-model="query"
              @keyup="getSearchData"
            />
          </div>
        </div>
      </div>
    </div>

    <button
      type="button"
      v-on:click="createMode"
      class="btn btn-primary btn-lg createButton"
    >
      Create
    </button>
    <table class="table sortable tab" id="my-table">
      <thead>
        <tr>
          <th scope="col" id="name" @click="sort('name')">
            Student Name
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="16"
              height="16"
              fill="currentColor"
              class="bi bi-arrow-down-up"
              viewBox="0 0 16 16"
            >
              <path
                fill-rule="evenodd"
                d="M11.5 15a.5.5 0 0 0 .5-.5V2.707l3.146 3.147a.5.5 0 0 0 .708-.708l-4-4a.5.5 0 0 0-.708 0l-4 4a.5.5 0 1 0 .708.708L11 2.707V14.5a.5.5 0 0 0 .5.5zm-7-14a.5.5 0 0 1 .5.5v11.793l3.146-3.147a.5.5 0 0 1 .708.708l-4 4a.5.5 0 0 1-.708 0l-4-4a.5.5 0 0 1 .708-.708L4 13.293V1.5a.5.5 0 0 1 .5-.5z"
              />
            </svg>
          </th>
          <th scope="col" @click="sort('emailId')">
            Email Id
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="16"
              height="16"
              fill="currentColor"
              class="bi bi-arrow-down-up"
              viewBox="0 0 16 16"
            >
              <path
                fill-rule="evenodd"
                d="M11.5 15a.5.5 0 0 0 .5-.5V2.707l3.146 3.147a.5.5 0 0 0 .708-.708l-4-4a.5.5 0 0 0-.708 0l-4 4a.5.5 0 1 0 .708.708L11 2.707V14.5a.5.5 0 0 0 .5.5zm-7-14a.5.5 0 0 1 .5.5v11.793l3.146-3.147a.5.5 0 0 1 .708.708l-4 4a.5.5 0 0 1-.708 0l-4-4a.5.5 0 0 1 .708-.708L4 13.293V1.5a.5.5 0 0 1 .5-.5z"
              />
            </svg>
          </th>
          <th scope="col" @click="sort('education')">
            Education
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="16"
              height="16"
              fill="currentColor"
              class="bi bi-arrow-down-up"
              viewBox="0 0 16 16"
            >
              <path
                fill-rule="evenodd"
                d="M11.5 15a.5.5 0 0 0 .5-.5V2.707l3.146 3.147a.5.5 0 0 0 .708-.708l-4-4a.5.5 0 0 0-.708 0l-4 4a.5.5 0 1 0 .708.708L11 2.707V14.5a.5.5 0 0 0 .5.5zm-7-14a.5.5 0 0 1 .5.5v11.793l3.146-3.147a.5.5 0 0 1 .708.708l-4 4a.5.5 0 0 1-.708 0l-4-4a.5.5 0 0 1 .708-.708L4 13.293V1.5a.5.5 0 0 1 .5-.5z"
              />
            </svg>
          </th>
          <th scope="col" @click="sort('mobile')">
            Mobile No
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="16"
              height="16"
              fill="currentColor"
              class="bi bi-arrow-down-up"
              viewBox="0 0 16 16"
            >
              <path
                fill-rule="evenodd"
                d="M11.5 15a.5.5 0 0 0 .5-.5V2.707l3.146 3.147a.5.5 0 0 0 .708-.708l-4-4a.5.5 0 0 0-.708 0l-4 4a.5.5 0 1 0 .708.708L11 2.707V14.5a.5.5 0 0 0 .5.5zm-7-14a.5.5 0 0 1 .5.5v11.793l3.146-3.147a.5.5 0 0 1 .708.708l-4 4a.5.5 0 0 1-.708 0l-4-4a.5.5 0 0 1 .708-.708L4 13.293V1.5a.5.5 0 0 1 .5-.5z"
              />
            </svg>
          </th>
          <th scope="col">Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(user, index) in users" v-bind:key="user.studentId">
          <td>{{ user.name }}</td>
          <td>{{ user.emailId }}</td>
          <td>{{ user.education }}</td>
          <td>{{ user.mobile }}</td>
          

          <td>
            <div
            
              style="cursor: pointer"
              class="dropdown"
              v-on:click="myFunction(user.emailId)"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                width="16"
                height="16"
                fill="currentColor"
                class="bi bi-three-dots-vertical"
                viewBox="0 0 16 16"
              >
                <path
                  d="M9.5 13a1.5 1.5 0 1 1-3 0 1.5 1.5 0 0 1 3 0zm0-5a1.5 1.5 0 1 1-3 0 1.5 1.5 0 0 1 3 0zm0-5a1.5 1.5 0 1 1-3 0 1.5 1.5 0 0 1 3 0z"
                />
              </svg>
              

              <div v-if="showOptions[user.emailId]" class="dropDown">
              
  

                <a
                  href="#"
                  class="dropAnchor"
                  v-on:click="popuptrue(user.studentId)"
                  >Delete</a
                >
                <br />
                

                <a href="#" class="dropAnchor" v-on:click="updateData(index)"
                  >Update</a
                >
                <!-- <a href="#"
                
                
                v-on:click="popuptrue(user.studentId)"
              >Delete
                </a
              >
              <br>

              <a href="#"
              
                
                v-on:click="updateData(index)"
              >
                Update
              </a> -->
              </div>
            </div>
          </td>
          <!-- <div v-if="showOptions[user.emailId]" >
              <button
                type="button"
                class="btn btn-danger"
                v-on:click="popuptrue(user.studentId)"
              >Delete
                </button
              ><br /><br />

              <button
                type="button"
                class="btn btn-info sty"
                v-on:click="updateData(index)"
              >
                UPDATE
              </button>
              </div> -->
        </tr>
      </tbody>
    </table>
    <div class="paginationStyle">
      <!-- <Pagination
        v-model="currentPage"
        :records="users.length"
        :per-page="pageSize"
        @paginate="filteredUsers.length"
      ></Pagination> -->
      <!-- <button type="button" class="btn btn-secondary" @click="handleChangeMinus">&lt;&lt;</button>
      <button v-for="pageNumber in Math.ceil(this.size / this.pageSize)"  @click="currentPage = pageNumber" v-bind:key="pageNumber">{{pageNumber}}</button>
      <button type="button" class="btn btn-primary" @click="handleChangePlus">&gt;&gt;</button> -->
      <!-- <button @click="handleChangeMinus">&lt;</button>
      
      

      <button @click="handleChangePlus">&gt;</button> -->
      <!-- <v-pagination v-model="currentPage" :pages="10" :range-size="1" active-color="#DCEDFF" @update:modelValue="filteredUsers"></v-pagination> -->
      <nav aria-label="Page navigation example" class="navPage">
  <ul class="pagination">
  <li class="page-item">
      <a class="page-link" href="#" aria-label="Previous" @click="onFirstPage()">
        <span aria-hidden="true">&lt;&lt;</span>
        <span class="sr-only"></span>
      </a>
    </li>
    <li class="page-item">
      <a class="page-link" href="#" aria-label="Previous" @click="handleChangeMinus">
        <span aria-hidden="true">&lt;</span>
        <span class="sr-only"></span>
      </a>
    </li>
    <div class="pa" v-for="pageNumber in Math.ceil(this.size / this.pageSize)"  @click="currentPage = pageNumber" v-bind:key="pageNumber">
    
    <li class="page-item"><a class="page-link" href="#" >{{pageNumber}}</a></li>
    </div>
    <li class="page-item">
      <a class="page-link" href="#" aria-label="Next" @click="handleChangePlus">
        <span aria-hidden="true">&gt;</span>
        <span class="sr-only"></span>
      </a>
    </li>
    <li class="page-item">
      <a class="page-link" href="#" aria-label="Next" @click="onLastPage()" >
        <span aria-hidden="true">&gt;&gt;</span>
        <span class="sr-only"></span>
      </a>
    </li>
  </ul>
</nav>
    </div>
  </div>

  <div v-if="popupshow" >
  <b-modal v-model="popupshow" v-on:click="deleted(studentId)">Are you sure you want to delete?

        
        
        
      
        
      
  </b-modal>
  
  <!-- <div >
  <a href="#" class="crossButton" v-on:click="popupfalse()"><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-x-circle" viewBox="0 0 16 16">
  <path d="M8 15A7 7 0 1 1 8 1a7 7 0 0 1 0 14zm0 1A8 8 0 1 0 8 0a8 8 0 0 0 0 16z"/>
  <path d="M4.646 4.646a.5.5 0 0 1 .708 0L8 7.293l2.646-2.647a.5.5 0 0 1 .708.708L8.707 8l2.647 2.646a.5.5 0 0 1-.708.708L8 8.707l-2.646 2.647a.5.5 0 0 1-.708-.708L7.293 8 4.646 5.354a.5.5 0 0 1 0-.708z"/>
</svg></a>
  </div>
    <br />
    <br />
    
    <h6>Are you sure you want to delete?</h6>
    <div class="thisDiv">
      <br />
      <button
        type="button"
        class="btn btn-primary popupButton"
        v-on:click="popupfalse()"
      >
        Cancel
      </button>
      <button
        type="button"
        class="btn btn-danger popupButton"
        v-on:click="deleted(studentId)"
      >
        Delete
      </button>
    </div> -->
    
  </div>

  <div v-if="createStudent" class="styling">
    <br />
    <br />
    <h3>Fill Student Details</h3>
    <br />

    <form v-on:submit="saveStudent">
      <b-alert v-model="failAlert" class="showError">{{
        alertMessage
      }}</b-alert>
      <br />
      <div class="form-group">
        <label for="name" class="nameMargin"><h2>Student Name</h2></label><br />
        <input
          class="form-control inputMargin"
          id="name"
          placeholder="Enter name"
          v-model="formData.name"
        />
      </div>
      <div class="form-group">
        <label for="emailId" class="emailDeco"><h2>Email Id</h2></label><br />
        <input
          class="form-control inputMargin"
          id="emailId"
          placeholder="Enter email"
          v-model="formData.emailId"
        />
      </div>
      <div class="form-group">
        <label for="education" class="marginOthers"><h2>Education</h2></label
        ><br />
        <input
          class="form-control inputMargin"
          id="education"
          placeholder="Enter education"
          v-model="formData.education"
        />
      </div>
      <div class="form-group">
        <label for="mobile" class="marginOthers"><h2>Mobile No</h2></label
        ><br />
        <input
          class="form-control inputMargin"
          id="mobile"
          placeholder="Enter mobile no"
          v-model="formData.mobile"
        />
      </div>
      <br />
      <br />
      <button
        type="button"
        class="btn btn-success buttonStyling"
        v-on:click="saveStudent()"
      >
        Save
      </button>
      <button
        type="button"
        class="btn btn-primary buttonStyling"
        v-on:click="cancel"
      >
        Cancel
      </button>
    </form>
  </div>
  <div v-if="updateForm" class="styling">
    <br />
    <br />
    <h3>Update Student Details</h3>

    <form v-on:submit="upDateSave">
      <div class="form-group">
        <label for="name" class="nameMargin"><h2>Student Name</h2></label><br />
        <input
          class="form-control inputMargin"
          id="name"
          v-model="tempUser.name"
        />
      </div>
      <div class="form-group">
        <label for="emailId" class="emailDeco"><h2>Email Id</h2></label><br />
        <input
          class="form-control inputMargin"
          id="emailId"
          v-model="tempUser.emailId"
          disabled
        />
      </div>
      <div class="form-group">
        <label for="education" class="marginOthers"><h2>Education</h2></label
        ><br />
        <input
          class="form-control inputMargin"
          id="education"
          v-model="tempUser.education"
        />
      </div>
      <div class="form-group">
        <label for="mobile" class="marginOthers"><h2>Mobile No</h2></label
        ><br />
        <input
          class="form-control inputMargin"
          id="mobile"
          v-model="tempUser.mobile"
        />
      </div>

      <br />
      <br />
      <button
        type="button"
        class="btn btn-success buttonStyling"
        v-on:click="upDateSave"
      >
        Save
      </button>
      <button
        type="button"
        class="btn btn-primary buttonStyling"
        v-on:click="cancel"
      >
        Cancel
      </button>
    </form>
  </div>
</template>
<script>
import axios from "axios";
// import VPagination from "@hennge/vue3-pagination";
import "@hennge/vue3-pagination/dist/vue3-pagination.css";


export default {
  name: "StudentData",
  data() {
    return {
      users: [],
      listStudent: true,
      createStudent: false,
      updateForm: false,
      tempUser: Object,
      formData: {},
      query: "",
      deleteid: "",
      originalusers: [],
      failAlert: false,
      alertMessage: "",
      popupshow: false,
      showOptions: {},
      sortValue: "",
      val: -1,
      pageSize: 4,
      currentPage: 1,
      count: 1,
      size: 0,
      numberOfStudents:0
    };
  },
  components: {
    
  },
  computed: {
    filteredUsers: function () {
      return this.users.filter((row, index) => {
        let start = (this.currentPage - 1) * this.pageSize;
        let end = this.currentPage * this.pageSize;
        if (index >= start && index < end) return true;
      });
    },
  },
  methods: {
    onFirstPage(){
      if(this.currentPage===1){
        return
      }
      else{
      this.currentPage=1;
      }

    },
    onLastPage(){
      if(this.currentPage===Math.ceil(this.size / this.pageSize)){
        return 
      }
      else{
        this.currentPage=Math.ceil(this.size / this.pageSize)
      }

    },
    handleChangePlus: function () {
      if(this.currentPage>=Math.ceil(this.size / this.pageSize)){
        var s = this.currentPage;
        this.currentPage = s;
      }
      else{
      this.currentPage = this.currentPage + 1;
      console.log(this.currentPage);
      }
    },

    handleChangeMinus: function () {
      if(this.currentPage != 1) this.currentPage = this.currentPage-1;
      console.log(this.currentPage);

    },

    showDropdown: function () {
      document.getElementById("myDropdown").classList.toggle("show");
    },
    nextPage: function () {
      if (this.currentPage * this.pageSize < this.users.length)
        this.currentPage++;
    },
    prevPage: function () {
      if (this.currentPage > 1) this.currentPage--;
    },
    myFunction(emailId) {
      this.showOptions[emailId] = !this.showOptions[emailId];
    },

    sort(s) {
      this.val = -1 * this.val;
      this.sortValue = s;
      this.users.sort((a, b) =>
        a[s].toLowerCase() > b[s].toLowerCase()
          ? this.val
          : b[s].toLowerCase() > a[s].toLowerCase()
          ? -1 * this.val
          : 0
      );
    },

    popupfalse() {
      this.popupshow = false;
    },
    popuptrue(id) {
      this.popupshow = true;
      this.deleteid = id;
    },

    // search() {
    //   var results = [];
    //   //var searchData = this.deleteidoriginalusers;
    //   if (this.query == "") {
    //     this.users = this.originalusers;
    //   } else {
    //     for (var i = 0; i < this.originalusers.length; i++) {
    //       var sparam = this.query.toLowerCase();

    //       for (var key in this.originalusers[i]) {
    //         if (this.originalusers[i]) {
    //           var value = this.originalusers[i][key];
    //           if (
    //             typeof value == "string" &&
    //             value.toLowerCase().indexOf(sparam) >= 0
    //           ) {
    //             results.push(this.originalusers[i]);
    //             break;
    //           }
    //         }
    //       }
    //     }
    //     this.users = results;
    //   }
    // },

    createMode() {
      this.listStudent = false;
      this.updateForm = false;
      this.createStudent = true;
    },
    cancel() {
      this.listStudent = true;
      this.updateForm = false;
      this.createStudent = false;
    },
    updateData(index) {
      this.listStudent = false;
      this.updateForm = true;
      this.createStudent = false;
      console.log("Temo user " + this.users[index]);
      this.tempUser = this.users[index];
    },
    getAllStudents() {
      axios
        .get(
          `http://localhost:9001/listStudents?limit=${this.pageSize}&offset=${this.currentPage}`
        )
        .then((response) => {
          console.log(response.data.data);
          this.users = response.data.data;
          this.originalusers = this.users;
          this.size = response.data.size
        })
        .catch((error) => {
          console.log(error);
        });
    },
    getSearchData() {
      axios
        .get(`http://localhost:9001/searchStudents/${this.query}`)
        .then((response) => {
          this.users = response.data.data;
          this.numberOfStudents = response.data.data.length;
          this.size = response.data.size;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    saveStudent() {
      axios
        .post("http://localhost:9001/addStudents", this.formData)
        .then((response) => {
          console.log(response.data.data);
          if (response.data.data == null) {
            this.showFailAlert();
          } else {
            this.getAllStudents();
            this.listStudent = true;
            this.updateForm = false;
            this.createStudent = false;
          }
        })
        .catch((error) => {
          console.log(error);
        });
    },
    showFailAlert() {
      this.failAlert = true;
      this.alertMessage = "Error : student already exists";
    },
    deleted() {
      this.deleteUser(this.deleteid);
      this.popupfalse();
    },

    deleteUser(studentId) {
      var req = {};
      req["studentId"] = studentId;

      axios
        .post("http://localhost:9001/deleteStudent", req)
        .then((response) => {
          console.log(response);
          this.getAllStudents();
        });
    },
    upDateSave() {
      var req = {};
      req["studentId"] = this.tempUser.studentId;
      req["name"] = this.tempUser.name;
      req["emailId"] = this.tempUser.emailId;
      req["mobile"] = this.tempUser.mobile;
      req["education"] = this.tempUser.education;
      axios
        .post("http://localhost:9001/updateStudents", req)

        .then((response) => {
          console.log(response);
          this.getAllStudents();
          this.listStudent = true;
          this.updateForm = false;
          this.createStudent = false;
        });
    },
  },
  mounted() {
    this.getAllStudents();
  },
  watch:{
    currentPage: function(){
      this.getAllStudents();
    },
    query: function(){
      if (this.query.length == 0){
        this.getAllStudents();
      }
    }
  }
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.createButton {
  margin-left: 1700px;
  margin-top: -80px;
}

.creatingStyle {
  margin-bottom: 30px;
}

.inputDecoration {
  font-size: 20px;
  margin-left: 10px;
  width: 800px;
  height: 40px;
  padding: 10px;
}
.buttonStyling {
  margin-right: 15px;
  margin-top: 20px;
}
.styling {
  background-color: gainsboro;
  height: 80vh;
  width: 60%;
  margin-left: 400px;
}

.search {
  position: relative;
  box-shadow: 0 0 40px rgba(51, 51, 51, 0.1);
}
.showError {
  font-size: 30px;
  margin: auto;
  color: rgb(212, 65, 65);
}

.search input {
  height: 60px;
  text-indent: 25px;
  border: 2px solid #d6d4d4;
}
.sty {
  border: 1px solid rgb(190, 189, 189);
}

.search input:focus {
  box-shadow: none;
  border: 2px solid blue;
}

.popupContainer {
  margin-bottom: 100px;
  width: 300px;
  height: 250px;
  position: absolute;
  left: 40%;
  right: 40%;
  bottom: 30%;
  background-color: rgb(238, 232, 232);
  opacity: 1;
  margin-right: 100px;
}

.pageDiv {
  margin-left: 80%;
}
.pageButton button {
  margin: 10px;
  padding: 10px;
}

.nameMargin {
  margin-left: -800px;
}
.inputMargin {
  width: 1000px;
  margin-left: 50px;
  margin-right: 50px;
  margin-top: 20px;
  height: 47px;
  margin-bottom: 20px;
}
.marginOthers {
  margin-left: -850px;
}
.thisDiv {
  margin-top: auto;
}
.popupButton {
  padding: 5px;
  margin: 10px;
}
.paginationStyle {
  margin-left: 1500px;
  margin-top: 30px;
}
.dropDown {
  padding: 15px;
  display: block;
  margin-right: 16px;
  position: absolute;
  box-shadow: 1px 1px 5px #5e5e5e;
  /* margin-right: 0px; */
  left: 93px;
  background-color: #ffffff;
  /* border: solid 1px black; */
  z-index: 2;
  margin-top: 10px;
}

.updateButton {
  margin-top: 5px;
}

.emailDeco {
  margin-left: -880px;
}
.paginationBtn {
  display: inline;
}
.dropAnchor {
  text-decoration: none;
  border: none;
  color: rgb(71, 67, 67);
}
.dropDown a:hover {
  color: rgb(93, 14, 167);
}
.pa{
  display: inline;
  

}
.crossButton{
  padding-left: 270px;
  color:rgb(71, 67, 67);
  
  
}
.crossButton:hover{
  color:rgb(179, 89, 89)

}
.navPage{
  margin-left:50px;

}

</style>


