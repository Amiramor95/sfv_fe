<template>
    <div id="layoutSidenav">
      <CommonSidebar />
      <div id="layoutSidenav_content">
        <CommonHeader />
        <main>
          <div class="container-fluid px-4">
            <div class="page-title">
              <h1>Senarai Pendaftaran Baharu Vaksin</h1>
              <a href="/app/modules/Vaccine/vaccine-new-registration" class="add-btn" title="Pendaftaran Baharu"><i class="fal fa-plus"></i></a>
            </div>
            <div class="card mb-4">
              <div class="card-body">
                <div class="search-table mt-2">
                  <div class="row">
                    <div class="col-sm-5 ml-auto mb-2 search-box">
                      <div class="input-group">
                        <span class="input-group-text" id="basic-addon1">
                          <i class="fa fa-search"></i>
                        </span>
                        <input
                          type="text"
                          class="form-control"
                          placeholder="Carian melalui nama vaksin atau status"
                          v-model="search"
                          @keyup="OnSearch"
                        />
                      </div>
                    </div>
                  </div>
                </div>
                <!-- search-table -->
                <table
                  class="table table-striped data-table font-13"
                  style="width: 100%"
                >
                  <thead>
                    <tr>
                      <th>Bil</th>
                      <th>Tarikh Permohonan</th>
                      <th>Nama Vaksin</th>
                      <th>Nama Pemohon</th>
                      <th>Tarikh Kemaskini</th>
                      <th>Status Permohonan</th>
                      <th>Tindakan</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr>
                      <td>1</td>
                      <td>13-08-2023</td>
                      <td>VAKSI JENIS 2</td>
                      <td>NURUL SAADAH BINTI MOHD SHARIFF</td>
                      <td>13-08-2023</td>
                      <td>DIKEMBALIKAN</td>
                      <td style="width: 5px;align-items: center;"> <a class="edit" @click="oneditPatient()"><i class="fa fa-edit"></i></a></td>
                    </tr>
                    <tr>
                      <td>1</td>
                      <td>10-04-2021</td>
                      <td>VAKSI JENIS 1</td>
                      <td>NURUL SAADAH BINTI MOHD SHARIFF</td>
                      <td>10-06-2023</td>
                      <td>DALAM PENILAIAN</td>
                      <td> <a class="view" @click="oneditPatient()"><i class="fa fa-eye"></i></a></td>
                    </tr>
                  </tbody>
                </table>
                <!--<p
                  v-show="!list.length"
                  style="
                    padding: 0px;
                    margin: 10px;
                    color: red;
                    display: flex;
                    justify-content: center;
                  "
                >
                  Tiada Rekod ditemui
                </p>-->
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
    name: "patient-list",
  
    data() {
      return {
        userdetails: null,
        list: [],
        branchlist: [],
        servicelist: [],
        userId: 0,
        token: "",
        keyword: "",
        search: "",
        search2: "",
        branch_id: 0,
        service_id: 0,
        assistancelist: [],
        dataReady: false,
        dataReady2: false,
      };
    },
    beforeMount() {
      this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
      this.getRole();
  
    },
    mounted() {
      this.GetList();
      const headers = {
        Authorization: "Bearer " + this.userdetails.access_token,
        Accept: "application/json",
        "Content-Type": "application/json",
      };
      const axios = require("axios").default;
      axios
        .get(
          `${this.$axios.defaults.baseURL}` +
            "patient-registration/getPatientRegistrationList",
          { headers }
        )
        .then((resp) => {
          this.list = resp.data.list;
          $(document).ready(function () {
            $(".data-table").DataTable({
              searching: false,
              bLengthChange: false,
              bInfo: false,
              autoWidth: false,
              responsive: true,
              language: {
                paginate: {
                  next: '<i class="fad fa-arrow-to-right"></i>', // or '→'
                  previous: '<i class="fad fa-arrow-to-left"></i>', // or '←'
                },
              },
            });
          });
        })
        .catch ((err) => {
          this.loader = false;
          this.$swal.fire({
                    icon: 'error',
                    title: 'Oops... Something Went Wrong!',
                    text: 'the error is: ' + err,
                    footer: ''
                  });
  
          console.error(err);
        });
  
         if(localStorage.getItem("keyword")!=''){
        this.search2=localStorage.getItem("keyword");
        this.search=this.search2;
        this.OnSearch();
      }
    },
    methods: {
      async getRole() {
        const headers = {
          Authorization: "Bearer " + this.userdetails.access_token,
          Accept: "application/json",
          "Content-Type": "application/json",
        };
        const response = await this.$axios.post(
          "staff-management/getRoleCode",
          { email: this.userdetails.user.email },
          {
            headers,
          }
        );
        this.branch_id=this.userdetails.branch.branch_id;
              if (response.data.list.code =="superadmin"){
                this.dataReady2= true;
                this.dataReady= false;
              }else{
                this.dataReady= true;
                this.dataReady2= false;
              }
  
      },
      async GetList() {
        const headers = {
          Authorization: "Bearer " + this.userdetails.access_token,
          Accept: "application/json",
          "Content-Type": "application/json",
        };
        const response1 = await this.$axios.get("service/list", { headers });
        if (response1.data.code == 200 || response1.data.code == "200") {
          this.servicelist = response1.data.list;
        } else {
          this.servicelist = [];
        }
        const response2 = await this.$axios.get("hospital/branch-list", {
          headers,
        });
        if (response2.data.code == 200 || response2.data.code == "200") {
          this.branchlist = response2.data.list;
        } else {
          this.branchlist = [];
        }
        const respons = await this.$axios.get(
          "general-setting/list?section=" + "assistance-or-supervision",
          { headers }
        );
        if (respons.data.code == 200 || respons.data.code == "200") {
          this.assistancelist = respons.data.list;
        } else {
          this.assistancelist = [];
        }
      },
      oneditPatient(Id) {
         if(this.SidebarAccess==1){
          this.$router.push({
          path: "/modules/Intervention/patient-summary",
          query: { id: Id },
        });
        }else{
        }
      },
      async OnSearch() {
        localStorage.removeItem('keyword');
        const headers = {
          Authorization: "Bearer " + this.userdetails.access_token,
          Accept: "application/json",
          "Content-Type": "application/json",
        };
        if (!this.search) {
          this.keyword = "no-keyword";
        } else {
          this.keyword = this.search;
        }
        const response = await this.$axios.post(
          "/patient/search",
          {
            keyword: this.keyword,
            branch_id: this.branch_id,
            service_id: this.service_id,
          },
          { headers }
        );
        if (response.data.code == 200) {
          if (response.data.list.length > 0) {
            this.list.splice(0, this.list.length);
            this.list = response.data.list;
  
          } else {
            this.list.splice(0, this.list.length);
            if ($.fn.DataTable.isDataTable(".data-table")) {
              $(".data-table").DataTable().clear().destroy();
            }
          }
        } else {
          this.$swal.fire({
                    icon: 'error',
                    title: 'Oops... Something Went Wrong!',
                    text: 'the error is: ' + this.error,
                    footer: ''
                  });
        }
      },
    },
  };
  </script>
  