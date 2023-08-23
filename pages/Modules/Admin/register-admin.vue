<template>
  <div id="layoutSidenav">
    <CommonSidebar />
    <div id="layoutSidenav_content">
      <CommonHeader />
      <main>
        <div class="container-fluid px-4">
          <div class="page-title">
            <h1>Senarai Pentadbir</h1>
            <div class="btn-group-a">
              <a href="/app/modules/Admin/sfv-new-staff" class="add-btn"><em class="fa fa-plus"></em></a>
            </div>
          </div>

          <div class="card mb-4">
            <div class="card-body">
              <div class="search-table">
                <div class="row mt-2">


                  <div class="col-lg-4 col-sm-6 mb-3">
                    <div class="input-group" style="position : relative; left: 100%;">
                      <span class="input-group-text bg-transparent br-0"
                        ><i class="fa fa-search"></i
                      ></span>
                      <input
                        type="text"
                        class="form-control"
                        placeholder="Carian Nama Pentadbir"
                        @keyup="onnamechange"
                      />
                    </div>
                  </div>
                </div>
              </div>
              <!-- search-table -->
              <div style="overflow-x:auto;">
                <table class="table table-striped data-table display nowrap" style="width: 100%">
                <thead>
                  <tr>
                    <th>No</th>
                    <th>Nama Pentadbir</th>
                    <th>Peranan</th>
                    <th>ID Pengguna</th>
                    <th>Emel</th>

                    <th>Status</th>
                    <th style="width:8%">Action</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(staff,index) in list" :key="index">
                    <td>{{ index+1}}</td>
                    <td>{{ staff.name }}</td>
                    <td>{{staff.role_name}}</td>
                    <td>{{staff.id_user}}</td>
                    <td>{{ staff.email }}</td>
                    <td><a v-if="staff.status == '1'">Aktif</a><a v-else-if="staff.status == '0'">Tidak Aktif</a></td>
                    <td>
                      <a @click="view(staff)" class="view" title="view staff profile"><em class="fa fa-eye"></em></a>
                    </td>
                  </tr>
                </tbody>
              </table>
              </div>

              <!-- <div class="card mb-4 reslt" style="display: none">
            <div class="card-body">
              <div style="overflow-x:auto;">
                <table class="table table-striped data-table display nowrap" style="width: 100%">
                <thead>
                  <tr>
                    <th>No</th>
                    <th>Nama Pentadbir</th>
                    <th>Peranan</th>
                    <th>ID Pengguna</th>
                    <th>Emel</th>
                    <th></th>
                    <th>Status</th>
                    <th style="width:8%">Action</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(staff,index) in list" :key="index">
                    <td>{{ index+1}}</td>
                    <td>{{ staff.name }}</td>
                    <td>{{staff.role_name}}</td>
                    <td>{{ staff.designation_name }}</td>
                    <td>{{ staff.hospital_branch_name }}</td>
                    <td>{{staff.service_name}}</td>
                    <td><a v-if="staff.status == '1'">Active</a><a v-else-if="staff.status == '0'">Inactive</a></td>
                    <td>
                      <a @click="view(staff)" class="view" title="view staff profile"><em class="fa fa-eye"></em></a>
                      <a class="view" @click="Onview(staff)" title="view user matrix"><em class="fa fa-bars"></em></a>
                    </td>
                  </tr>
                </tbody>
              </table>
              </div>
            </div>
          </div> -->

            </div>
          </div>
        </div>
      </main>
    </div>
  </div>
</template>
<script>
import CommonHeader from '../../../components/CommonHeader.vue';
import CommonSidebar from '../../../components/CommonSidebar.vue';
export default {
  components: { CommonSidebar, CommonHeader },
  name: "staff-management",
  setup() {},
  head: {
    script: [

      {
        src: "https://cdnjs.cloudflare.com/ajax/libs/jspdf/1.3.2/jspdf.min.js",
        async: true,
        crossorigin: "anonymous",
      },
    ],
  },
  data() {
    return {
      userdetails: null,
      list: [],
      SidebarAccess:null,
    };
  },

  mounted() {
    this.GetList();

  },

  beforeMount() {
    this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
    this.SidebarAccess = JSON.parse(localStorage.getItem("SidebarAccess"));
  },
  methods: {

    async GetList() {
      const headers = {
        Authorization: "Bearer " + this.userdetails.access_token,
        Accept: "application/json",
        "Content-Type": "application/json",
      };
      const response = await this.$axios.post(
        "staff-management/getStaffManagementListOrByEmail",
        { email: this.userdetails.user.email},
        {
          headers,
        }
      );
      if (response.data.code == 200 || response.data.code == "200") {
        this.list = response.data.list;
      } else {
        this.list = [];
      }
    },
    async view(data) {
      this.$router.push({
        path: "/modules/Admin/staff-view",
        query: { id: data.id },
      });
    },

    async onnamechange(event) {

      this.userdetails.branch.branch_name = event.target.value;
      this.GetList();
    },

    OnPrint() {
      var newstr = document.getElementsByClassName("reslt")[0].innerHTML;
      document.body.innerHTML = newstr;
      window.print();
      window.location.reload();
    },
    downloadform() {
      setTimeout(() => {
        this.$refs.result.classList.remove("hide");
        var pdf = new jsPDF("p", "pt", "a4");
        pdf.addHTML($("#result")[0], function () {
          pdf.save("userid-request-form.pdf");
        });
      }, 100);
      setTimeout(() => {
        this.$refs.result.classList.add("hide");
      }, 100);
    },
    Onview(data) {

      this.$router.push({
        path: "/modules/Admin/list-of-user-matrix-view",
      query: {id: data.service_name, usersid:data.users_id },
      });
      },
    },
};
</script>
<style scoped>
h4.form-sub-title {
  font-size: 14px;
  letter-spacing: 1px;
  font-weight: 600;
  color: #000;
}

.form-group-box {
  margin-bottom: 40px;
}
.form-group-box .form-group {
  margin-bottom: 0px;
}
.form-group-box .form-control {
  border-radius: 0px;
  border-color: #000;
  margin-bottom: -1px;
}
.form-group-box .form-textarea {
  resize: none;
  min-height: 110px;
}

.form-group-box p {
  text-transform: none;
  font-size: 13px;
  font-weight: 500;
  margin: 20px 0;
}
.form-header-box {
  border-bottom: 1px solid #ddd;
  padding-bottom: 10px;
}
.form-header-box h1 {
  text-align: center;
  font-size: 20px;
  font-weight: 600;
  letter-spacing: 0.5px;
}
.form-header-box img {
  width: 100%;
}
.h5-title {
  text-align: center;
  font-size: 15px;
  font-weight: 600;
  margin: 20px 0 40px;
  letter-spacing: 1px;
}
.hide {
  display: none !important;
}

.my-custom-class{
  /* position: absolute; */
  right: 0;
}
</style>
