<template>
    <div id="layoutSidenav">
        <CommonSidebar />
        <div id="layoutSidenav_content">
            <CommonHeader />
            <main>
                <div class="container-fluid px-4 dashboard">
                    <div class="page-title dashboard-title">
                        <h1>DASHBOARD</h1>
                    </div>
                     <div class="row">
                        <div class="col-sm-6 mb-3">
                            <div class="card">
                                <div class="card-details">
                                    <img src="~/assets/images/schedule.png">
                                    <div class="text">
                                        <h1>{{ permohonan }}</h1>
                                        <p>Jumlah Permohonan Vaksin</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="col-sm-6 mb-3">
                            <div class="card">
                                <div class="card-details">
                                    <img src="~/assets/images/man.png">
                                    <div class="text">
                                        <h1>{{ pemohon }}</h1>
                                        <p>Jumlah Pengguna</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="col-sm-6 mb-3">
                            <div class="card">
                                <div class="card-details">
                                    <img src="~/assets/images/team.png">
                                    <div class="text">
                                        <h1>{{ pentadbir }}</h1>
                                        <p>Jumlah Admin Pentadbir</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="col-sm-6 mb-3">
                            <div class="card">
                                <div class="card-details">
                                    <img src="~/assets/images/team.png">
                                    <div class="text">
                                        <h1>{{ penyemak }}</h1>
                                        <p>Jumlah Penyemak</p>
                                    </div>
                                </div>
                            </div>
                        </div>

                    </div>


          

                    <div class="row">
                        <div class="col-sm-12">
                            <div class="card mt-4 mb-3">
                                <div class="card-header dashboard-header">
                                    <h4>PENGUMUMAN:</h4>
                                </div>
                                <table class="announcement-table">
                                    <tbody>
                                        <tr>
                                            <div v-if="index < list.length" v-for="(ann,index) in AnnouncmentToShow" :key="index">
                                                    <td><span class="number">{{ index+1 }}</span></td>
                                                    <td><a v-bind:href="announcement_route+ list[ann-1].id">{{ list[ann-1].title }} ({{ getFormattedDate(list[ann-1].start_date) }})</a></td>
                                            </div>
                                            <div v-if="AnnouncmentToShow< list.length || list.length > AnnouncmentToShow">
                                                    <button class="btn btn-primary btn-text btn-seeall" @click="AnnouncmentToShow += 5">Show More</button>
                                            </div>
                                        </tr>
                                        <!-- <tr>
                                            <td><span class="number">02</span></td>
                                            <td>Hari Kesihatan Mental</td>
                                        </tr> -->
                                    </tbody>
                                </table>
                            </div>
                        </div>
                    </div>
                    <!-- row -->
                </div>
            </main>
        </div>
    </div>
</template>
<script>
import moment from 'moment';
import CommonHeader from '../../../components/CommonHeader.vue';
import CommonSidebar from '../../../components/CommonSidebar.vue';
export default {
    components: { CommonSidebar, CommonHeader },
    name: "admin-dashboard",
    data() {
        return {
            userdetails: null,
            permohonan: "0",
            penyemak: "0",
            pentadbir: "0",
            pemohon: "0",
            list: [],
            cd_draft:[],
            review_patient:[],
            AnnouncmentToShow:3,
            totalAnouncement:0,
            search:'',
            announcement_route:'',
            review_route:'',
        };
    },
    beforeMount() {
        this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
      this.id=this.userdetails.user.id;
      this.email=this.userdetails.user.email;
      this.name=this.userdetails.user.name;

    },
    mounted(){
      this.Getrecord();


    },

    methods: {
        async Getrecord() {
                const headers = {
                    Authorization: "Bearer " + this.userdetails.access_token,
                    Accept: "application/json",
                    "Content-Type": "application/json",
                };
                const response = await this.$axios.post(
                    "all-mentari-staff/post",
                    {email:this.email},
                    {
                    headers,
                    }
                );
                if (response.data.code == 200 || response.data.code == "200") {
                    this.permohonan= response.data.permohonan;
                    this.penyemak= response.data.penyemak;
                    this.pentadbir= response.data.pentadbir;
                    this.pemohon= response.data.pengguna;

          
                } else {
                    this.list = [];
                }
            },

        getFormattedDate(date) {
            return moment(date).format("DD-MM-YYYY")
        },

        SearchPatient() {

            localStorage.setItem('keyword',(this.search));
            this.$router.push("/modules/Patient/patient-list" );
        },
    },
};
</script>
