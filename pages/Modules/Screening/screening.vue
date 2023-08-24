<template>
  <div id="layoutSidenav">
    <CommonSidebar />
    <div id="layoutSidenav_content">
      <CommonHeader />
      <main>
        <div class="container-fluid px-4">
          <div class="page-title">
            <h1>Senarai Proses Saringan</h1>
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
              <table  class="table table-striped data-table font-13" style="width: 100%">
                <thead>
                    <tr>
                      <th>Bil</th>
                      <th>Tarikh Permohonan</th>
                      <th>Nama Vaksin</th>
                      <th>Nama Pemohon</th>
                      <th>Tarikh Kemaskini</th>
                      <th>Status Saringan</th>
                      <th>Tindakan</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(vaccine,index) in vaccines" :key="index"> <!--this list is retrieved from vaccine_reg joined with multiple tables-->
                      <td>{{ index+1 }}</td>
                      <td>{{ vaccine.created_at }}</td> <!--from "vaccine_reg" table-->
                      <td>{{ vaccine.vac_name }}</td> <!--from "admin_info" table -->
                      <td>{{ vaccine.name }}</td> <!-- from "staff_management" table-->
                      <td>{{ vaccine.updated_at }}</td> <!--from "vaccine_reg" table-->
                      <td>{{ vaccine.status }}</td><!--from "vaccine_reg" table-->
                      <td>some buttons</td>
                    </tr>
                </tbody>
              </table>
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
    name: "screening",
  
    data(){
      return{
        userdetails: null,
        vaccines: [],
        search: "",
      };
    },

    beforeMount(){
      this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
    },

    methods:{
      async getList(){
        const headers = {
          Authorization: "Bearer " + this.userdetails.access_token,
          Accept: "application/json",
          "Content-Type": "application/json",
        };
        const response = await this.$axios.get("screening/list", { headers });
        if (response.data.code == 200 || response.data.code == "200") {
          this.vaccines = response.data.list;
        } else {
          this.vaccines = [];
        }
      },
    },
  }

</script>
