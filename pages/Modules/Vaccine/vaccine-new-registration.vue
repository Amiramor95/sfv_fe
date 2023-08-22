<template>
  <div id="layoutSidenav">
      <CommonSidebar />
      <div id="layoutSidenav_content">
          <CommonHeader />
          <main>
          <Loader v-if="loader" />
          <div class="container-fluid px-4">
          <div class="page-title"><h1>Pendaftaran Baharu Vaksin</h1></div>
          <div class="card mb-4">
            <div class="card-body">
              <div>
                <div class="accordion form-accordion mt-3" id="accordionExample">
                  <div class="accordion-item">
                    <h2 class="accordion-header" id="headingOne">
                      <button
                        class="accordion-button collapsed"
                        type="button"
                        data-bs-toggle="collapse"
                        data-bs-target="#collapseOne"
                        aria-expanded="false"
                        aria-controls="collapseOne">
                        BAHAGIAN I : MAKLUMAT PENGURUSAN (<span style="font-style:italic;color: grey;font-size: small;">PART I: ADMINISTRATIVE INFORMATION </span>)
                      </button>
                        
                    </h2>
                    <div
                      id="collapseOne"
                      class="accordion-collapse collapse"
                      aria-labelledby="headingOne"
                      data-bs-parent="#accordionExample">
                      <div class="accordion-body">
                        <table class="notes">
                          <tbody>
                            <tr>
                              <th>Nama Penuh Pemohon <br> <span style="font-style:italic;color: grey;font-size: smaller;">Full Name of Applicant </span></th>
                              <td style="width: 2%;">:</td>
                              <td>NURUL SAADAH BINTI MOHD SHARIFF</td>
                            </tr>
                            <tr>
                              <th>Nombor Kad Pengenalan<br> <span style="font-style:italic;color: grey;font-size: smaller;">Identification Card (IC) Number of Applicant</span></th>
                              <td>:</td>
                              <td>890408-03-5256</td>
                            </tr>
                            <tr>
                              <th>Alamat<br> <span style="font-style:italic;color: grey;font-size: smaller;">Address</span> </th>
                              <td>:</td>
                              <td>NO 53,Jalan Kajang Perdana 2/5, Taman Kajang Perdana, 43000 Kajang</td>
                            </tr>
                            <tr>
                              <th>Nama Pengilang Vaksin<br> <span style="font-style:italic;color: grey;font-size: smaller;">Name of Vaccine Manufacturer</span> </th>
                              <td>:</td>
                              <td>ABC Manufacture</td>
                            </tr>
                            <tr>
                              <th>Nombor Pendaftaran Pengilang Vaksin Yang telah didaftarkan oleh DVS<br> <span style="font-style:italic;color: grey;font-size: smaller;">DVS Manufacturer Registration Number</span> </th>
                              <td>:</td>
                              <td>M100023</td>
                            </tr>
                            <tr>
                              <th>Nama Vaksin<br> <span style="font-style:italic;color: grey;font-size: smaller;">Name of Vaccine</span> </th>
                              <td>:</td>
                              <td><input type="text" v-model="vaccine_name" class="form-control" style="width: 100%;"></td>
                            </tr>
                            <tr>
                              <th>Penyakit yang disasarkan<br> <span style="font-style:italic;color: grey;font-size: smaller;">Target Disease</span> </th>
                              <td>:</td>
                              <td><textarea v-model="target_disease" rows="2" class="form-control"></textarea></td>
                            </tr>
                            <tr>
                              <th>Spesies yang disasarkan<br> <span style="font-style:italic;color: grey;font-size: smaller;">Target Species</span> </th>
                              <td>:</td>
                              <td><textarea v-model="target_species" rows="2" class="form-control"></textarea></td>
                            </tr>
                          </tbody>
                        </table>
                      </div>
                    </div>
                  </div>
                  <!--  -->
                  <div class="accordion-item">
                    <h2 class="accordion-header" id="headingTwo">
                      <button
                        class="accordion-button collapsed"
                        type="button"
                        data-bs-toggle="collapse"
                        data-bs-target="#collapseTwo"
                        aria-expanded="false"
                        aria-controls="collapseTwo"
                      >
                        BAHAGIAN II : MAKLUMAT BAHAN MULA (<span style="font-style:italic;color: grey;font-size: small;">PART II: STARTING MATERIAL INFORMATION </span>)
                      </button>
                    </h2>
                    <div
                      id="collapseTwo"
                      class="accordion-collapse collapse"
                      aria-labelledby="headingTwo"
                      data-bs-parent="#accordionExample"
                    >
                      <div class="accordion-body">
                        <div class="col-md-12 mb-3">
                          <label class="form-label">Medication</label>
                          <textarea
                            class="form-control textarea"
                            placeholder="Please Type Prescription Here"
                            v-model="medication_des"
                          ></textarea>
                        </div>
                      </div>
                    </div>
                  </div>
                  <div class="accordion-item">
                    <h2 class="accordion-header" id="headingThree">
                      <button
                        class="accordion-button collapsed"
                        type="button"
                        data-bs-toggle="collapse"
                        data-bs-target="#collapseThree"
                        aria-expanded="false"
                        aria-controls="collapseThree"
                      >
                        BAHAGIAN III : PENGHASILAN DAN PENILAIAN VAKSIN (<span style="font-style:italic;color: grey;font-size: small;">PART III: VACCINES PRODUCTION &
EVALUATION </span>)
                      </button>
                    </h2>
                    <div
                      id="collapseTwo"
                      class="accordion-collapse collapse"
                      aria-labelledby="headingThree"
                      data-bs-parent="#accordionExample"
                    >
                      <div class="accordion-body">
                        <div class="col-md-12 mb-3">
                          <label class="form-label">Medication</label>
                          <textarea
                            class="form-control textarea"
                            placeholder="Please Type Prescription Here"
                           
                          ></textarea>
                        </div>
                      </div>
                    </div>
                  </div>
                  <div class="accordion-item">
                    <h2 class="accordion-header" id="headingThree">
                      <button
                        class="accordion-button collapsed"
                        type="button"
                        data-bs-toggle="collapse"
                        data-bs-target="#collapseThree"
                        aria-expanded="false"
                        aria-controls="collapseThree"
                      >
                      BAHAGIAN IV: PRODUK SIAP (<span style="font-style:italic;color: grey;font-size: small;">PART IV: FINISHED PRODUCT </span>)
                      </button>
                    </h2>
                    <div
                      id="collapseTwo"
                      class="accordion-collapse collapse"
                      aria-labelledby="headingThree"
                      data-bs-parent="#accordionExample"
                    >
                      <div class="accordion-body">
                        <div class="col-md-12 mb-3">
                          <label class="form-label">Medication</label>
                          <textarea
                            class="form-control textarea"
                            placeholder="Please Type Prescription Here"
                           
                          ></textarea>
                        </div>
                      </div>
                    </div>
                  </div>
                  <!--  -->
                </div>
                       <br><br>
                <div class="d-flex">
                    <button
                      @click=""
                      class="btn btn-primary btn-text"
                      ><i class="fa fa-arrow-alt-to-left"></i> Back
                    </button>
                    <div  class="btn-right">
                    <button type="submit" @click="" class="btn btn-warning btn-text">
                      <i class="fa fa-save"></i> Simpan Draft
                    </button>

                    <button type="submit" @click="" class="btn btn-warning btn-text ml-auto">
                      <i class="fa fa-paper-plane"></i> Simpan & Hantar Permohonan
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
          </main>
          <intervention-footer></intervention-footer>
      </div>
  </div>
  </template>
  
  <script>
  import CommonHeader from '../../../components/CommonHeader.vue';
  import CommonSidebar from '../../../components/CommonSidebar.vue';
  export default {
      components: {
          CommonHeader,
          CommonSidebar
      },
      name: "vaccine registration",
      data() {
          return {
              userdetails: null,
            
              loader: false,
             
          };
      },
      beforeMount() {
          this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
          
      },
      methods: {
         
          
      },
  };
  </script>
  
  <style scoped>
  .hide {
      display: none;
  }
  
  #nav-tab a {
      pointer-events: none;
  }
  </style>
  