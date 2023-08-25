<template>
  <div id="layoutSidenav">
    <CommonSidebar />
    <div id="layoutSidenav_content">
      <CommonHeader />
      <main>
        <div class="container-fluid px-4">
          <div class="page-title">
            <h1>Pengurusan Pentadbiran</h1>
          </div>
          <div class="card mb-4">
            <div class="card-header">
              <h4>Butiran Pentadbir</h4>
            </div>
            <div class="card-body">
              <table
                class="info-table event-info mt-3"
                width="100%"
                v-if="staffdetail"
              >
                <thead>
                  <tr>
                    <th width="40%"></th>
                    <th width="60%"></th>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <td>Nama</td>
                    <td>{{ staffdetail.name }}</td>
                  </tr>
                  <tr>
                    <td>Alamat Emel</td>
                    <td>{{ staffdetail.email }}</td>
                  </tr>
                  <tr>
                    <td>Peranan</td>
                    <td>{{ staffdetail.role }}</td>
                  </tr>
                  <tr>
                    <td>ID Pengguna</td>
                    <td>{{ staffdetail.id_user }}</td>
                  </tr>
                  <tr>
                    <td>Status Akaun</td>
                    <td v-if="staffdetail.status==1">Active</td>
                    <td v-if="staffdetail.status==0">Non-active account</td>
                  </tr>

                </tbody>
              </table>

              <div class="form-foter mt-3">
                <button @click="back" type="button" class="btn btn-primary btn-fill btn-md">
                    <i class="fa fa-step-backward"/> &nbsp; Back
                </button>
              </div>
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
  name: "staff-transfer",
  setup() {},
  data() {
    return {
      Id: 0,
      url:"",
      userdetails: null,
      staffdetail: null,
    };
  },
  beforeMount() {
    this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
    let urlParams = new URLSearchParams(window.location.search);
    this.Id = urlParams.get("id");
    this.getDetails();
  },
  methods: {
    async getDetails() {
      const headers = {
        Authorization: "Bearer " + this.userdetails.access_token,
        Accept: "application/json",
        "Content-Type": "application/json",
      };
      const response = await this.$axios.post(
        "staff-management/getDetailsById",
        { id: this.Id },
        {
          headers,
        }
      );
      console.log("list", response.data);
      if (response.data.code == 200 || response.data.code == "200") {
        this.staffdetail = response.data.list[0];
      } else {
        this.staffdetail = [];
      }
    },
    async gotoedit(){
     this.$router.push({
        path: "/modules/Admin/edit-staff",
        query: { id: this.Id },
      });
    },
    async gototransfer(){
     this.$router.push({
        path: "/modules/Admin/mentari-staff-transfer",
        query: { id: this.Id },
      });
    },
     async deletestaff() {
      const headers = {
        Authorization: "Bearer " + this.userdetails.access_token,
        Accept: "application/json",
        "Content-Type": "application/json",
      };
      const response = await this.$axios.post(
        "staff-management/remove",
        {
          added_by: this.userdetails.user.id,
          id: this.Id,
        },
        { headers }
      );
      if (response.data.code == 200) {
        this.$router.push("/modules/Admin/staff-management");
      } else {this.$swal.fire({
                  icon: 'error',
                  title: 'Oops... Something Went Wrong!',
                  text: 'the error is: ' + JSON.stringify(response.data.message),
                  footer: ''
                });
      }
    },
    back() {
      this.$router.go(-1);
    },
  },
};
</script>
