<template>
  <div id="layoutSidenav">
    <CommonSidebar />
    <div id="layoutSidenav_content">
      <CommonHeader />
      <main>
        <div class="container-fluid px-4">
          <div class="page-title">
            <h1>Pengurusan Pentadbir</h1>
          </div>
          <div class="card mb-4">
            <div class="card-header">
              <h4>Edit Pentadbir</h4>
            </div>
            <div class="card-body">
              <form class="g-3 mt-3" method="post" @submit.prevent="onCreateStaff">
                <div class="row">
                  <div class="col-md-6 mb-4">
                    <label for="" class="form-label">Nama</label>
                    <input type="text" class="form-control" placeholder="Enter Name" v-model="name" disabled/>
                  </div>
                  <div class="col-md-6 mb-4">
                    <label class="form-label">Alamat Emel</label>
                    <input type="text" class="form-control" placeholder="Enter Email Address" v-model="email" disabled/>
                  </div>

                </div>
                <!-- close-row -->

                <div class="row">
                  <div class="col-md-6 mb-4">
                    <label for="" class="form-label">ID Pengguna</label>
                    <input type="text" class="form-control" placeholder="Enter Profession Reg No."
                      v-model="professionregno" disabled/>
                  </div>

                  <div class="col-md-4 mb-4">
                    <label for="" class="form-label">Peranan</label>
                    <select v-model="roleId" class="form-select" aria-label="Default select example">
                      <option value="0">Sila Pilih</option>
                      <option v-for="role in rolelist" v-bind:key="role.id" v-bind:value="role.id">
                        {{ role.role_name }}
                      </option>
                    </select>
                  </div>
                </div>

                <!-- close-row -->
                <p v-if="errors.length">
                <ul>
                  <li style="color:red" v-for='err in errors' :key='err'>
                    {{ err }}
                  </li>
                </ul>
                </p>
                <div class="form-foter mt-3">
                  <a href="/app/modules/Admin/register-admin" class="btn btn-primary btn-text"><i
                      class="fa fa-arrow-alt-to-left"></i> Back</a>
                  <div class="btn-right">
                    <button type="submit" class="btn btn-warning btn-text">
                      <i class="fa fa-save"></i> Save
                    </button>
                  </div>
                </div>
              </form>
            </div>
          </div>
        </div>
      </main>
    </div>
  </div>
</template>
<script>
import CommonHeader from "../../../components/CommonHeader.vue";
import CommonSidebar from "../../../components/CommonSidebar.vue";
export default {
  components: { CommonSidebar, CommonHeader },
  name: "new-staff",
  data() {
    return {
      Id: 0,
      name: "",
      nricno: "",
      professionregno: "",
      roleId: 0,
      email: "",
      accountStatus: "",
      userdetails: null,
      rolelist: [],
      teamlist: [],
      designationlist: [],
      branchlist: [],
      errors: [],
    };
  },
  beforeMount() {
    this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
    let urlParams = new URLSearchParams(window.location.search);
    this.Id = urlParams.get("id");
    this.GetroleList();
    this.GetteamList();
    this.GetbranchList();
    this.GetdesignationList();
    this.Getdetails();
  },
  methods: {
    async Getdetails() {
      const headers = {
        Authorization: "Bearer " + this.userdetails.access_token,
        Accept: "application/json",
        "Content-Type": "application/json",
      };
      const response = await this.$axios.post(
        "staff-management/getDetailsById",
        { id: this.Id },
        { headers }
      );
      console.log("all resp", response.data);
      console.log("my details", response.data.list[0].name);
      if (response.data.code == 200 || response.data.code == "200") {

        this.name = response.data.list[0].name;
        this.professionregno = response.data.list[0].id_user;
        this.roleId = response.data.list[0].role_id;
        this.email = response.data.list[0].email;
        this.accountStatus = response.data.list[0].status;
      }
    },
    async GetroleList() {
      const headers = {
        Authorization: "Bearer " + this.userdetails.access_token,
        Accept: "application/json",
        "Content-Type": "application/json",
      };
      const response = await this.$axios.get("roles/branch-viewlist", { headers });
      this.rolelist = response.data.list;
    },
    async GetteamList() {
      const headers = {
        Authorization: "Bearer " + this.userdetails.access_token,
        Accept: "application/json",
        "Content-Type": "application/json",
      };
      const response = await this.$axios.get("service/list", {
        headers,
      });
      if (response.data.code == 200 || response.data.code == "200") {
        this.teamlist = response.data.list;
      } else {
        this.teamlist = [];
      }
    },
    async GetbranchList() {
      const headers = {
        Authorization: "Bearer " + this.userdetails.access_token,
        Accept: "application/json",
        "Content-Type": "application/json",
      };
      const response = await this.$axios.get("hospital/branch-list", {
        headers,
      });
      if (response.data.code == 200 || response.data.code == "200") {
        this.branchlist = response.data.list;
      } else {
        this.branchlist = [];
      }
    },
    async GetdesignationList() {
      const headers = {
        Authorization: "Bearer " + this.userdetails.access_token,
        Accept: "application/json",
        "Content-Type": "application/json",
      };
      const response = await this.$axios.get(
        "general-setting/list?section=" + "designation",
        {
          headers,
        }
      );
      if (response.data.code == 200 || response.data.code == "200") {
        this.designationlist = response.data.list;
      } else {
        this.designationlist = [];
      }
    },

    async onCreateStaff() {
      if (confirm("Are you sure you want to update this record")) {
        this.errors = [];
        if (!this.name) {
          this.errors.push("Name is required.");
        }
        if (this.roleId <= 0) {
          this.errors.push("Role  is required.");
        }
        if (!this.email) {
          this.errors.push("Email is required.");
        }else {

          const headers = {
            Authorization: "Bearer " + this.userdetails.access_token,
            Accept: "application/json",
            "Content-Type": "application/json",
          };
          let body = new FormData();
          body.append("id", this.Id);
          body.append("added_by", this.userdetails.user.id);
          body.append("name", this.name);
          body.append("id_user", this.professionregno);
          body.append("role_id", this.roleId);
          body.append("email", this.email);
          const response = await this.$axios.post(
            "staff-management/AdminUpdate",
            body,
            {
              headers,
            }
          );
          if (response.data.code == 200 || response.data.code == "200") {
            this.$swal.fire(
              'Successfully Updated',
            );
            this.$router.push("/modules/Admin/register-admin");
          } else {
            this.$swal.fire({
              icon: 'error',
              title: 'Oops... Something Went Wrong!',
              text: 'the error is: ' + this.error,
              footer: ''
            });
          }
        }
      }
    },
  },
};
</script>
