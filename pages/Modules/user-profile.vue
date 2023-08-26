<template>
    <div id="layoutSidenav">
        <CommonSidebar />
        <div id="layoutSidenav_content">
            <CommonHeader />
            <main>
                <div class="container-fluid px-4">
                    <div class="page-title">
                        <h1>Kemas Kini Profil</h1>
  
                    </div>
                    <div class="row">
                        <div class="card mb-4">
                            <div class="card-body">
                                <nav>
                                    <ul id="nav-tab" role="tablist" class="nav sub-tab">
                                        <li class="nav-item">
                                            <a data-bs-toggle="tab" href="#nav-home1" role="tab" aria-controls="nav-home" aria-selected="true" class="nav-link active">
                                                Profil Pengguna</a>
                                        </li>
                                    </ul>
                                </nav>
                                <div id="nav-tabContent" class="tab-content"></div>
                                <div id="nav-home1" role="tabpanel" class="tab-pane fade show active">
                                    <div class="content-subtab">
                                        <form class="g-3 mt-3" method="post" @submit.prevent="onUpdateProfile">
                                            <div class="row">
                                                <div class="col-md-6 mb-4">
                                                    <label for="" class="form-label">Nama Penuh<span style="color:red">*</span></label>
                                                    <input type="text" class="form-control" placeholder="Nama Penuh" v-model="name" />
                                                </div>
                                                <div class="col-md-6 mb-4">
                                                    <label for="" class="form-label">ID Pengguna<span style="color:red">*</span></label>
                                                    <input type="text" class="form-control" placeholder="Nama Penuh" v-model="id_user" />
                                                </div>

                                            </div>

  
                                            <div class="row">
                                                <div class="col-md-6 mb-4">
                                                    <label for="" class="form-label">Alamat Emel<span style="color:red">*</span></label>
                                                    <input type="text" class="form-control" placeholder="Isi Alamat Emel" v-model="email" />
                                                </div>
                                                <div class="col-md-3 mb-4">
                                                    <label for="" class="form-label">No. Telefon</label>
                                                    <input type="text" :maxlength="11" oninput="javascript: if (this.value.length > this.maxLength) this.value = this.value.slice(0, this.maxLength);" 
                                                    class="form-control" placeholder="Isi No. Telefon." v-model="contactno" />
                                                </div>
                                            </div>

                                            <br>
                                            <br>
                                            <div class="form-foter mt-3">
                                                <a @click="back" class="btn btn-primary btn-text"><i class="fa fa-arrow-alt-to-left"></i> Kembali</a>
                                                <div class="ml-auto" id="hidebutton" ref="hidebutton">
                                                      <button type="submit" class="btn btn-warning btn-text" >
                                                          <i class="fa fa-save"></i> Simpan
                                                      </button>
                                                  </div>
                                            </div>
                                        </form>
                                    </div>
                                </div>
  
                            </div>
                        </div>
                    </div>
                </div>
            </main>
        </div>
    </div>
    </template>
  
    <script>
    import { relativeTimeThreshold } from "moment";
  import CommonHeader from "../../components/CommonHeader.vue";
    import CommonSidebar from "../../components/CommonSidebar.vue";
    export default {
        components: {
            CommonSidebar,
            CommonHeader
        },
        name: "new-staff",
        data() {
            return {
                name: "",
                email: "",
                email_old:"",
                contactno: "",
                id_user: "",
                userdetails: null,
                nricerror: null,
                SidebarAccess: null,
                errors: []
            };
        },
        beforeMount() {
            this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
            this.SidebarAccess = JSON.parse(localStorage.getItem("SidebarAccess"));
            this.email_old = this.userdetails.user.email;
        },
        mounted() {
  
            this.GetUserDetails();

        },
        methods: {

            back(){
            this.$router.go(-1);
          },
            async GetUserDetails() {
                const headers = {
                    Authorization: "Bearer " + this.userdetails.access_token,
                    Accept: "application/json",
                    "Content-Type": "application/json",
                };
                const response = await this.$axios.post(
                    "staff-management/UserProfile",
                    { email: this.email_old},
                    {
                    headers,
                    }
                );
                if (response.data.code == 200 || response.data.code == "200") {
                    this.email = response.data.list[0].email;
                    this.id_user =response.data.list[0].id_user;
                    this.name = response.data.list[0].name;
                    this.contactno = response.data.list[0].contact_no;
          
                    this.getCity();
                    this.getPostcode();
                } else {
                    this.list = [];
                }
            },
  
            async onUpdateProfile() {
  
        this.$swal.fire({
            title: 'Adakah Anda Pasti?',
            text: "Perubahan Tidak Boleh Dibatalkan!",
            icon: 'warning',
            showCancelButton: true,
            confirmButtonText: 'Setuju!',
            cancelButtonText: 'Batal!',
            reverseButtons: true
        }).then(async (result) => {
            if (result.isConfirmed) {
                this.errors = [];
                if (!this.name) {
                    this.errors.push("Nama Penuh Pemohon adalah diperlukan.");
                }
                if (!this.id_user) {
                    this.errors.push("Nama Penuh Pemohon adalah diperlukan.");
                }
                if (!this.email) {
                    this.errors.push("Alamat Emel adalah diperlukan.");
                }
                if (
                    (this.name &&
                        this.email &&
                        this.id_user  
                        )
                ) {
                    this.loader = true;
                    const headers = {
                        Authorization: "Bearer " + this.userdetails.access_token,
                        Accept: "application/json",
                        "Content-Type": "application/json",
                    };
                    let body = new FormData();
                    body.append("name", this.name);
                    body.append("poscode", this.PostCode);
                    body.append("email", this.email);
                    body.append("id_user", this.id_user);
                    body.append("contact_no", this.contactno);
                    body.append("email_old",this.email_old);
        
                        const response = await this.$axios.post(
                        "staff-management/UserUpdateProfile",
                        body,
                        {
                            headers,
                        }
                    );
                        if (response.data.code == 200 || response.data.code == "200") {
                            this.loader = false;
                            await this.$swal.fire(
                                'Kemaskini Profil Telah Berjaya.',
                                'Data Telah DiSimpan.',
                                'success',
                            );
                            if(this.email_old!=this.email){
                                localStorage.removeItem('userdetails');
                                this.$router.push("/staff-login");
                            }else{
                                this.$router.push("/Modules/user-profile");
                            }

                        } else {
                            this.loader = false;
            
                            this.$swal.fire({
                                icon: 'error',
                                title: 'Oops... Something Went Wrong!',
                                text: 'the error is: ' + JSON.stringify(response.data.message),
                            });
                        }
                    }
      }
  })
  },
  
        },
    };
    </script>
  
    <style scoped>
    .hide {
        display: none !important;
    }
    </style>
  