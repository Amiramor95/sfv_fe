<template>
    <div id="layoutSidenav">
        <CommonSidebar />
        <div id="layoutSidenav_content">
            <CommonHeader />
            <main>
                <div class="container-fluid px-4">
                    <div class="page-title">
                        <h1>Pengurusan Pengguna</h1>
                        <!-- <a href="#"><i class="fal fa-plus"></i> Add</a> -->
                    </div>
                    <div class="row">
                        <div class="card mb-4">
                            <div class="card-body">
                                <nav>
                                    <ul id="nav-tab" role="tablist" class="nav sub-tab">
                                        <li class="nav-item">
                                            <a data-bs-toggle="tab" href="#nav-home1" role="tab" aria-controls="nav-home" aria-selected="true" class="nav-link active">
                                                Daftar Pengguna Baru</a>
                                        </li>
                                    </ul>
                                </nav>
                                <div id="nav-tabContent" class="tab-content"></div>
                                <div id="nav-home1" role="tabpanel" class="tab-pane fade show active">
                                    <div class="content-subtab">
                                        <form class="g-3 mt-3" method="post" @submit.prevent="onCreateStaff">
                                            <div class="row">
                                                <div class="col-md-6 mb-4">
                                                    <label for="" class="form-label">Nama Penuh Pemohon<span style="color:red">*</span></label>
                                                    <input type="text" class="form-control" placeholder="Nama Penuh" v-model="name" v-on:keypress="isLetter($event)" />
                                                </div>
    
                                                <div class="col-md-4 mb-4">
                                                    <label for="" class="form-label">No. Kad Pengenalan Pemohon<span style="color:red">*</span></label>
                                                    <input type="text" :maxlength="12" class="form-control" placeholder="No. Kad Pengenalan" v-model="nricno" v-on:keypress="NumbersOnly" />
                                                    <Error :message="nricerror" v-if="nricerror" />
                                                </div>
    
                                            </div>
                                            <!-- close-row -->
    
                                            <div class="row">
    
                                                <div class="col-md-6 mb-4">
                                                    <label for="" class="form-label">Alamat Lengkap Pemohon</label>
                                                    <input type="text" class="form-control mb-3" placeholder="Alamat Lengkap" v-model="BranchAddress1" />
    
                                                    <input type="text" class="form-control mb-3" placeholder="Alamat Lengkap" v-model="BranchAddress2" />
    
                                                    <input type="text" class="form-control" placeholder="Alamat Lengkap" v-model="BranchAddress3" />
                                                </div>
    
                                                <div class="col-md-6">
                                                    <label for="" class="form-label">Negeri</label>
                                                    <select v-model="State" class="form-select" aria-label="Default select example" @change="onCitybind($event)">
                                                        <option value="0">Sila Pilih</option>
                                                        <option v-for="state in StateList" v-bind:key="state.id" v-bind:value="state.id">
                                                            {{ state.state_name }}
                                                        </option>
                                                    </select>
    
                                                    <div class="row mt-4">
                                                        <div class="col-md-6">
                                                            <label for="" class="form-label">Bandar</label>
                                                            <select v-model="City" class="form-select" aria-label="Default select example" @change="onPostbind($event)">
                                                                <option value="0">Sila Pilih</option>
                                                                <option v-for="ctl in CityList" v-bind:key="ctl.city_name" v-bind:value="ctl.city_name">
                                                                    {{ ctl.city_name }}
                                                                </option>
                                                            </select>
                                                        </div>
    
                                                        <div class="col-md-6">
                                                            <label for="" class="form-label">Poskod</label>
                                                            <select v-model="PostCode" class="form-select" aria-label="Default select example">
                                                                <option value="0">Sila Pilih</option>
                                                                <option v-for="pst in PostCodeList" v-bind:key="pst.id" v-bind:value="pst.id">
                                                                    {{ pst.postcode }}
                                                                </option>
                                                            </select>
                                                        </div>
                                                    </div>
                                                </div>
    
                                            </div>
                                            <!-- close-row -->
    
                                            <div class="row">
                                                <div class="col-md-6 mb-4">
                                                    <label for="" class="form-label">Alamat Emel<span style="color:red">*</span></label>
                                                    <input type="text" class="form-control" placeholder="Isi Alamat Emel" v-model="email" @blur="validateEmail" />
                                                </div>
                                                <div class="col-md-3 mb-4">
                                                    <label for="" class="form-label">No. Telefon<span style="color:red">*</span></label>
                                                    <input type="text" :maxlength="11" oninput="javascript: if (this.value.length > this.maxLength) this.value = this.value.slice(0, this.maxLength);" class="form-control" placeholder="Isi No. Telefon." v-model="contactno" v-on:keypress="NumbersOnly" />
                                                </div>
                                                <div class="col-md-3 mb-4">
                                                    <label for="" class="form-label">Peranan<span style="color:red">*</span></label>
    
                                                    <input type="text" :maxlength="11" oninput="javascript: if (this.value.length > this.maxLength) this.value = this.value.slice(0, this.maxLength);" class="form-control" v-model="rolelist2" v-on:keypress="NumbersOnly" disabled />
    
                                                </div>
                                            </div>
                                            <!-- close-row -->
    
                                            <div class="row">
                                                <!-- <div class="col-md-6 mb-4">
                            <label for="" class="form-label"
                              >ID Pengguna<span style="color:red">*</span></label
                            >
                            <input
                              type="text"
                              class="form-control"
                              placeholder="Isi ID Pengguna"
                              v-model="professionregno"
                            />
                          </div>
                          <div class="col-md-4 mb-4">
                            <label for="" class="form-label">Kata Laluan<span style="color:red">*</span></label>
                              <input
                                class="form-control"
                                id="inputPassword"
                                type="password"
                                placeholder="Isi Kata Laluan"
                                v-model="password"
                              />
    
                          </div> -->
                                                <div class="row">
                                                    <div class="col-md-6 mb-4">
                                                        <label for="" class="form-label">Jenis Pemilik<span style="color:red">*</span></label>
                                                        <select class="form-select" aria-label="Default select example" v-model="owner_type">
                                                            <option value="0">Sila Pilih</option>
                                                            <option value="Pemilik Kilang Vaksin (Tempatan)">Pemilik Kilang Vaksin (Tempatan)</option>
                                                            <option value="Pemilik Syarikat Pengimport">Pemilik Syarikat Pengimport</option>
                                                            <option value="Pemilik Syarikat Pengedar">Pemilik Syarikat Pengedar</option>
                                                            <option value="Pemilik Syarikat Penjual">Pemilik Syarikat Penjual</option>
                                                            <option value="Doktor Veterinar (Pengedar/Penjual)">Doktor Veterinar (Pengedar/Penjual)</option>
                                                        </select>
                                                    </div>
                                                </div>
    
                                                <div class="row">
                                                    <div class="col-md-6 mb-4">
                                                        <label for="" class="form-label">Nama Kilang<span style="color:red">*</span></label>
                                                        <input type="text" class="form-control" placeholder="Isi Nama Kilang" v-model="factory_name" />
                                                    </div>
    
                                                    <div class="col-md-6 mb-4">
                                                        <label for="" class="form-label">Alamat Kilang<span style="color:red">*</span></label>
                                                        <input type="text" class="form-control" placeholder="Isi Alamat Kilang" v-model="factory_addr" />
                                                    </div>
                                                </div>
    
                                            </div>
                                            <!-- close-row -->
    
                                            <!-- close-row -->
                                            <p v-if="errors.length">
                                                <ul>
                                                    <li style="color:red" v-for='err in errors' :key='err'>
                                                        {{ err }}
                                                    </li>
                                                </ul>
                                            </p>
                                            <br>
                                            <br>
                                            <div class="form-foter mt-3">
                                                <a href="/app/modules/Admin/staff-management" class="btn btn-primary btn-text"><i class="fa fa-arrow-alt-to-left"></i> Kembali</a>
                                                <div class="ml-auto" id="hidebutton" ref="hidebutton">
                                                    <button type="submit" class="btn btn-warning btn-text">
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
    import CommonHeader from "../../../components/CommonHeader.vue";
    import CommonSidebar from "../../../components/CommonSidebar.vue";
    export default {
        components: {
            CommonSidebar,
            CommonHeader
        },
        name: "new-staff",
        data() {
            return {
                name: "",
                nricno: "",
                BranchAddress1: "",
                BranchAddress2: "",
                BranchAddress3: "",
                State: "",
                City: "",
                PostCode: "",
                email: "",
                contactno: "",
                owner_type: "",
                factory_name: "",
                factory_addr: "",
                userdetails: null,
                StateList: [],
                CityList: [],
                PostCodeList: [],
                rolelist2: "",
                rolelist_id: 0,
                errors: [],
                nricerror: null,
                SidebarAccess: null,
            };
        },
        beforeMount() {
            this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
            this.SidebarAccess = JSON.parse(localStorage.getItem("SidebarAccess"));
            this.GetroleList();
            this.GetList();
        },
        mounted() {
            if (this.SidebarAccess != 1) {
                this.$refs.hidebutton.classList.add("hide");
            }
        },
        methods: {
            async GetList() {
                const headers = {
                    Authorization: "Bearer " + this.userdetails.access_token,
                    Accept: "application/json",
                    "Content-Type": "application/json",
                };
                const response5 = await this.$axios.get("address/list", {
                    headers
                });
                if (response5.data.code == 200 || response5.data.code == "200") {
                    this.StateList = response5.data.list;
                    this.CityList = [];
                    this.PostCodeList = [];
                } else {
                    this.StateList = [];
                    this.CityList = [];
                    this.PostCodeList = [];
                }
            },
            async onCitybind(event) {
                const headers = {
                    Accept: "application/json",
                    "Content-Type": "application/json",
                };
                const response = await this.$axios.post(
                    "address/" + event.target.value + "/getCityList", {
                        headers
                    }
                );
                if (response.data.code == 200 || response.data.code == "200") {
                    this.CityList = response.data.list;
                    this.PostCodeList = [];
                } else {
                    this.CityList = [];
                    this.PostCodeList = [];
                }
            },
            async onPostbind(event) {
                const headers = {
                    Authorization: "Bearer " + this.userdetails.access_token,
                    Accept: "application/json",
                    "Content-Type": "application/json",
                };
                const response = await this.$axios.post(
                    "address/" + event.target.value + "/getPostcodeListById", {
                        headers
                    }
                );
                if (response.data.code == 200 || response.data.code == "200") {
                    this.PostCodeList = response.data.list;
                } else {
                    this.PostCodeList = [];
                }
            },
            async GetroleList() {
                const headers = {
                    Authorization: "Bearer " + this.userdetails.access_token,
                    Accept: "application/json",
                    "Content-Type": "application/json",
                };
                const response = await this.$axios.get("roles/branch-viewlist", {
                    headers,
                });
                this.rolelist2 = response.data.list2[0].role_name;
                this.rolelist_id = response.data.list2[0].id;
              },
            async onCreateStaff() {
    
                this.$swal.fire({
                    title: 'Are you sure to save this?',
                    text: "You won't be able to revert this!",
                    icon: 'warning',
                    showCancelButton: true,
                    confirmButtonText: 'Yes, save it!',
                    cancelButtonText: 'No, cancel!',
                    reverseButtons: true
                }).then(async (result) => {
                    if (result.isConfirmed) {
                        this.errors = [];
                        if (!this.name) {
                            this.errors.push("Nama Penuh Pemohon adalah diperlukan.");
                        }
                        if (!this.nricno) {
                            this.errors.push("No. Kad Pengenalan Pemohon adalah diperlukan.");
                        }
                        if (!this.BranchAddress1) {
                            this.errors.push("Alamat Lengkap Pemohon Baris 1 adalah diperlukan.")
                        }
                        if (!this.BranchAddress2) {
                            this.errors.push("Alamat Lengkap Pemohon Baris 2 adalah diperlukan.")
                        }
                        if (!this.BranchAddress3) {
                            this.errors.push("Alamat Lengkap Pemohon Baris 3 adalah diperlukan.")
                        }
                        if (!this.State) {
                            this.errors.push("Negeri adalah diperlukan.")
                        }
                        if (!this.City) {
                            this.errors.push("Bandar adalah diperlukan.")
                        }
                        if (!this.PostCode) {
                            this.errors.push("Poskod adalah diperlukan.")
                        }
                        if (!this.email) {
                            this.errors.push("Alamat Emel adalah diperlukan.");
                        }
                        if (!this.contactno) {
                            this.errors.push("No. Telefon adalah diperlukan.");
                        }
                        if (!this.rolelist_id) {
                            this.errors.push("Peranan adalah diperlukan.");
                        }
                        if (!this.owner_type) {
                            this.errors.push("Jenis Pemilikan adalah diperlukan.");
                        }
                        if (!this.factory_name) {
                            this.errors.push("Nama Kilang adalah diperlukan")
                        }
                        if (!this.factory_addr) {
                            this.errors.push("Alamat Kilang adalah diperlukan")
                        }
                        if (
                            (this.name &&
                                this.nricno &&
                                this.BranchAddress1 &&
                                this.BranchAddress2 &&
                                this.BranchAddress3 &&
                                this.State &&
                                this.City &&
                                this.PostCode &&
                                this.rolelist_id &&
                                this.email &&
                                this.contactno &&
                                this.owner_type &&
                                this.factory_name &&
                                this.factory_addr &&
                                !this.nricerror)
                        ) {
                            this.loader = true;
                            const headers = {
                                Authorization: "Bearer " + this.userdetails.access_token,
                                Accept: "application/json",
                                "Content-Type": "application/json",
                            };
                            let body = new FormData();
                            body.append("added_by", this.userdetails.user.id);
                            body.append("name", this.name);
                            body.append("nric_no", this.nricno);
                            body.append("address_1", this.BranchAddress1);
                            body.append("address_2", this.BranchAddress2);
                            body.append("address_3", this.BranchAddress3);
                            body.append("state", this.State);
                            body.append("city", this.City);
                            body.append("postcode", this.PostCode);
                            body.append("email", this.email);
                            body.append("role_id", this.rolelist_id);
                            body.append("contact_no", this.contactno);
                            body.append("owner_type", this.owner_type); //check
                            body.append("name_vacs_manufacturer", this.factory_name);
                            body.append("address_vacs_factory", this.factory_addr);
                            const response = await this.$axios.post(
                                "staff-management/UserAdd",
                                body, {
                                    headers,
                                }
                            );
                            if (response.data.code == 200 || response.data.code == "200") {
                                this.loader = false;
                                await this.$swal.fire(
                                    'Successfully Submitted.',
                                    'Data is inserted.',
                                    'success',
                                );
                                this.$router.push("/Modules/Admin/staff-management");
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
    
            async validateEmail() {
                if (/^\w+([\.-]?\w+)@\w+([\.-]?\w+)(\.\w{2,3})+$/.test(this.email)) {
                    this.emailerror = null;
                } else {
                    this.emailerror = "Please Enter Valid Email";
                    this.email = "";
                }
            },
            async isLetter(e) {
                let char = String.fromCharCode(e.keyCode);
                if (/^[A-Za-z\'@ ]+$/.test(char)) return true;
                else e.preventDefault();
            },
    
            NumbersOnly(evt) {
                evt = (evt) ? evt : window.event;
                var charCode = (evt.which) ? evt.which : evt.keyCode;
                if ((charCode > 31 && (charCode < 48 || charCode > 57)) && charCode !== 46) {
                    evt.preventDefault();;
                } else {
                    return true;
                }
            },
    
            async CheckNric(event) {
                console.log("my body", event.target.value);
                const headers = {
                    Authorization: "Bearer " + this.userdetails.access_token,
                    Accept: "application/json",
                    "Content-Type": "application/json",
                };
                const response = await this.$axios.post(
                    "staff-management/checknricno", {
                        nric_no: event.target.value
                    }, {
                        headers
                    }
                );
                console.log("response", response.data);
                if (response.data.code == 200) {
                    this.nricerror = "NRIC No already exists";
                } else {
                    this.nricerror = null;
                }
            },
        },
    };
    </script>
    
    <style scoped>
    .hide {
        display: none !important;
    }
    </style>