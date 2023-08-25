<template>
    <div id="layoutSidenav">
        <CommonSidebar />
        <div id="layoutSidenav_content">
            <CommonHeader />
            <main>
                <div class="container-fluid px-4">
                    <div class="page-title">
                        <h1>Pengurusan Pengguna</h1>

                    </div>
                    <div class="row">
                        <div class="card mb-4">
                            <div class="card-body">
                                <nav>
                                    <ul id="nav-tab" role="tablist" class="nav sub-tab">
                                        <li class="nav-item">
                                            <a data-bs-toggle="tab" href="#nav-home1" role="tab" aria-controls="nav-home" aria-selected="true" class="nav-link active">
                                                Maklumat Pengguna</a>
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
                                                    <input type="text" disabled class="form-control" placeholder="Nama Penuh" v-model="name" />
                                                </div>

                                                <div class="col-md-4 mb-4">
                                                    <label for="" class="form-label">No. Kad Pengenalan Pemohon<span style="color:red">*</span></label>
                                                    <input disabled type="text" :maxlength="12" class="form-control" placeholder="No. Kad Pengenalan" v-model="nricno" />
                                                </div>

                                            </div>
                                            <!-- close-row -->

                                            <div class="row">

                                                <div class="col-md-6 mb-4">
                                                    <label for="" class="form-label">Alamat Lengkap Pemohon</label>
                                                    <input disabled type="text" class="form-control mb-3" placeholder="Alamat Lengkap" v-model="BranchAddress1" />

                                                    <input disabled type="text" class="form-control mb-3" placeholder="Alamat Lengkap" v-model="BranchAddress2" />

                                                    <input disabled type="text" class="form-control" placeholder="Alamat Lengkap" v-model="BranchAddress3" />
                                                </div>

                                                <div class="col-md-6">
                                                    <label for="" class="form-label">Negeri</label>
                                                    <select disabled v-model="State" class="form-select" aria-label="Default select example">
                                                        <option v-for="state in StateList" v-bind:key="state.id" v-bind:value="state.id">
                                                            {{ state.state_name }}
                                                        </option>
                                                    </select>

                                                    <div class="row mt-4">
                                                        <div class="col-md-6">
                                                            <label for="" class="form-label">Bandar</label>
                                                            <select disabled v-model="City" class="form-select" aria-label="Default select example">
                                                                <option value="0">Sila Pilih</option>
                                                                <option v-for="ctl in CityList" v-bind:key="ctl.city_name" v-bind:value="ctl.city_name">
                                                                    {{ ctl.city_name }}
                                                                </option>
                                                            </select>
                                                        </div>

                                                        <div class="col-md-6">
                                                            <label for="" class="form-label">Poskod</label>
                                                            <select disabled v-model="PostCode" class="form-select" aria-label="Default select example">
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
                                                    <input disabled type="text" class="form-control" placeholder="Isi Alamat Emel" v-model="email" />
                                                </div>
                                                <div class="col-md-3 mb-4">
                                                    <label for="" class="form-label">No. Telefon<span style="color:red">*</span></label>
                                                    <input disabled type="text" :maxlength="11" oninput="javascript: if (this.value.length > this.maxLength) this.value = this.value.slice(0, this.maxLength);" class="form-control" placeholder="Isi No. Telefon." v-model="contactno" />
                                                </div>
                                                <div class="col-md-3 mb-4">
                                                    <label for="" class="form-label">Peranan<span style="color:red">*</span></label>

                                                    <input disabled type="text" :maxlength="11" oninput="javascript: if (this.value.length > this.maxLength) this.value = this.value.slice(0, this.maxLength);" class="form-control" v-model="rolelist2"/>

                                                </div>
                                            </div>
                                            <!-- close-row -->

                                            <div class="row">

                                                <div class="row">
                                                    <div class="col-md-6 mb-4">
                                                        <label for="" class="form-label">Jenis Pemilik<span style="color:red">*</span></label>
                                                        <input disabled type="text" class="form-control" placeholder="Jenis Pemilik" v-model="factory_name" />
                                                    </div>
                                                </div>

                                                <div class="row">
                                                    <div class="col-md-6 mb-4">
                                                        <label for="" class="form-label">Nama Kilang<span style="color:red">*</span></label>
                                                        <input disabled type="text" class="form-control" placeholder="Isi Nama Kilang" v-model="factory_name" />
                                                    </div>

                                                    <div class="col-md-6 mb-4">
                                                        <label for="" class="form-label">Alamat Kilang<span style="color:red">*</span></label>
                                                        <input disabled type="text" class="form-control" placeholder="Isi Alamat Kilang" v-model="factory_addr" />
                                                    </div>
                                                </div>

                                            </div>
                                            <!-- close-row -->

                                            <!-- close-row -->
                                            <br>
                                            <br>
                                            <div class="form-foter mt-3">
                                                <a href="/app/modules/Admin/user-registration" class="btn btn-primary btn-text"><i class="fa fa-arrow-alt-to-left"></i> Kembali</a>
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
                State: 0,
                City: "",
                Postcode: "",
                StateList: [],
                CityList: [],
                PostCodeList: [],
                email: "",
                contactno: "",
                company_name: "",
                factory_name: "",
                factory_addr: "",
                userdetails: null,
                rolelist2: "",
                rolelist_id: 0,
                teamlist: [],
                designationlist: [],
                branchlist: [],
                errors: [],
                list:[],
                nricerror: null,
                SidebarAccess: null,
            };
        },
        beforeMount() {
            this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
            this.SidebarAccess = JSON.parse(localStorage.getItem("SidebarAccess"));
            let urlParams = new URLSearchParams(window.location.search);
            this.Id = urlParams.get("id");
        },
        mounted() {

            this.GetUserDetails();
            this.GetroleList()
            this.GetList();
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
            async getCity() {
            const headers = {
                Authorization: "Bearer " + this.userdetails.access_token,
                Accept: "application/json",
                "Content-Type": "application/json",
            };
            const response = await this.$axios.post(
                "address/" + this.State + "/getCityList", {
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
        async getPostcode() {
            const headers = {
                Accept: "application/json",
                "Content-Type": "application/json",
            };
            const response = await this.$axios.post(
                "address/" + this.City + "/getPostcodeListById", {
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
            async GetUserDetails() {
                const headers = {
                    Authorization: "Bearer " + this.userdetails.access_token,
                    Accept: "application/json",
                    "Content-Type": "application/json",
                };
                const response = await this.$axios.post(
                    "staff-management/UserDetail",
                    { id: this.Id},
                    {
                    headers,
                    }
                );
                if (response.data.code == 200 || response.data.code == "200") {
                   this.list = response.data.list[0];
                    this.email = this.list.email;
                    this.nricno = response.data.list[0].nric_no;
                    this.BranchAddress1 = response.data.list[0].address_1;
                    this.BranchAddress2 = response.data.list[0].address_2;
                    this.BranchAddress3 = response.data.list[0].address_3;
                    this.City = response.data.list[0].city
                    this.State = response.data.list[0].state;
                    this.PostCode = response.data.list[0].poscode;
                    this.name = response.data.list[0].name;
                    this.contactno = response.data.list[0].contact_no;
                    // this.rolelist2 = response.data.list2[0].role_name;
                    this.owner_type = response.data.list[0].owner_type;
                    this.factory_name = response.data.list[0].name_vacs_manufacturer;
                    this.factory_addr = response.data.list[0].address_vacs_factory;
                    this.getCity();
                    this.getPostcode();
                } else {
                    this.list = [];
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
