<template>
  <div class="card mb-4">
    <div class="card-header bg-transparent">
      <h4>Tetapan Peranan</h4>
    </div>
    <div class="card-body">
      <ul class="nav sub-tab" id="nav-tab" role="tablist">
        <li class="nav-item">
          <a class="nav-link active" data-bs-toggle="tab" href="#nav-Module" role="tab" aria-controls="nav-Module"
            aria-selected="true"><i class="far fa-user-lock"></i> Tetapan 1: Peranan Pengguna</a>
        </li>
      </ul>
      <div class="tab-content" id="nav-tabContent">
        <div class="tab-pane fade show active" id="nav-Module" role="tabpanel">
      <form method="post" @submit.prevent="onAddparameter()">
        <div class="content-subtab">
          <div class="filter-form">
            <div class="row mt-3">
              <div class="col-sm-6 mb-3">
                <label class="form-label">Nama Peranan</label>
                <input
                          type="text"
                          class="form-control"
                          placeholder="Masukkan Nama Peranan"
                          v-model="rolename"/>
              </div>

              <div class="col-sm-3 mb-4">
                        <label for="" class="form-label">Status</label>
                        <select class="form-select" v-model="rolestatus">
                          <option value="">Pilih Status</option>
                                <option value="0">Aktif</option>
                                <option value="1">Tidak Aktif</option>
                        </select>
                      </div>
            </div>
            <p v-if="errors.length">
                    <ul><li style="color:red"  v-for='err in errors' :key='err'>{{ err }}</li></ul>
                    </p>

                    <div class="d-flex justify-content-center" id="hidebutton1" ref="hidebutton1">
                      <button type="submit" class="btn btn-warning btn-text" v-if="Id"><i class="fa fa-save"></i>Simpan</button>
                      <button type="submit" class="btn btn-warning btn-text" v-if="!Id"><i class="fa fa-plus"></i> Tambah Parameter</button>
                    </div>

                    <div class="table-title">
                    <h3>Senarai Peranan</h3>
                  </div>
                  <table class="table table-striped data-table1 display nowrap" style="width: 100%">
                    <thead>
                      <tr>
                        <th style="width:3%">No</th>
                        <th>Nama Peranan</th>
                        <th>Status</th>
                        <th style="width:5%">Tindakan</th>
                      </tr>
                    </thead>
                    <tbody>
                      <tr v-for="(rg, index) in list" :key="index">
                        <td>{{index+1}}</td>
                        <td>{{rg.role_name}}</td>
                        <td>
                          <p v-if="rg.status == 0">Aktif</p>
                          <p v-if="rg.status == 1">Tidak Aktif</p>
                        </td>
                        <td>
                          <a class="edit" @click="editreg(rg)"><i class="fa fa-edit"></i></a>

                        </td>
                      </tr>
                    </tbody>
                  </table>
          </div>
        </div>
      </form>
    </div>
    </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "rolesetting",
  data() {
    return {
      rolename: "",
      rolestatus: 0,
      list: [],
      errors: [],
      userdetails: null,
      Id: 0,
    };
  },
  mounted() {
    this.GetList();
  },
  beforeMount() {
    this.userdetails = JSON.parse(localStorage.getItem("userdetails"));

  },
  methods: {
    async GetList() {
      const headers = {
      Authorization: "Bearer " + this.userdetails.access_token,
      Accept: "application/json",
      "Content-Type": "application/json",
    };
    const axios = require("axios").default;
    axios .get(`${this.$axios.defaults.baseURL}` + "roles/list", { headers })
      .then((resp) => {
        this.list = resp.data.list;
        $(document).ready(function () {
          $(".data-table1").DataTable({
            searching: false,
            bLengthChange: false,
            bInfo: false,
            // autoWidth: false,
            // responsive: true,
            scrollX: true,
            language: {
              paginate: {
                next: '<i class="fad fa-arrow-to-right"></i>', // or '→'
                previous: '<i class="fad fa-arrow-to-left"></i>', // or '←'
              },
            },
          });
           $('button[data-bs-toggle="tab"]').on("shown.bs.tab", function (e) {
            $($.fn.dataTable.tables(true))
              .DataTable()
              .columns.adjust()
              .responsive.recalc();
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

    },
    async onAddparameter() {
      if (confirm("Are you sure you want to save this entry")) {
      this.errors = [];
      try {
        if (!this.rolename) {
          this.errors.push("Role Name is required.");
        }
        if(this.rolename)
        {
          const headers = {
            Authorization: "Bearer " + this.userdetails.access_token,
            Accept: "application/json",
            "Content-Type": "application/json",
          };
          if (this.Id <= 0) {
            const response = await this.$axios.post(
              "roles/add",
              {
                requested_by: this.userdetails.user.id,
                role_name: this.rolename,
                status: this.rolestatus,
              },
              { headers }
            );
            if (response.data.code == 200 || response.data.code == "200") {
              this.$swal.fire('Successfully Update', '', 'success');
              this.resetmodel();
            } else {
              this.$swal.fire({
                  icon: 'error',
                  title: 'Oops... Something Went Wrong!',
                  text: 'the error is: ' + this.error,
                  footer: ''
                });
            }
          } else {
            const response = await this.$axios.post(
              "roles/update",
              {
                requested_by: this.userdetails.user.id,
                role_id: this.Id,
                role_name: this.rolename,
                status: this.rolestatus,
              },
              { headers }
            );

            if (response.data.code == 200 || response.data.code == "200") {
this.$swal.fire(
                  'Successfully Update',
                );
              this.resetmodel();
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
      } catch (e) {
        this.errors.push = e;
      }
    }
    },

    async editreg(data) {
      const headers = {
        Authorization: "Bearer " + this.userdetails.access_token,
        Accept: "application/json",
        "Content-Type": "application/json",
      };
      const response = await this.$axios.post(
        "roles/role-byId",
        {
          id: data.id,
        },
        { headers }
      );
      if (response.data.code == 200) {
        this.rolename = response.data.list[0].role_name;
        this.rolestatus = response.data.list[0].status;
        this.Id = data.id;
      } else {
        this.$swal.fire({
                  icon: 'error',
                  title: 'Oops... Something Went Wrong!',
                  text: 'the error is: ' + this.error,
                  footer: ''
                });
      }
    },

    async resetmodel() {
      this.rolename = "";
      this.rolestatus = "";
      this.errors = [];
      this.GetList();
      this.Id = 0;
    },



  },
};
</script>

