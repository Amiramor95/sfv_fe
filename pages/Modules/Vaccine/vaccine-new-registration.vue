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
                              <td colspan="3" style="color: black;font-weight: bold;">Seksyen A (Maklumat Umum)/Section A (General Information)</td>
                            </tr>
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
                            <tr>
                              <th>Keadaan Penyakit<br> <span style="font-style:italic;color: grey;font-size: smaller;">Nature of Disease</span> </th>
                              <td>:</td>
                              <td>
                                <div class="form-check">
                                    <input
                                      class="form-check-input"
                                      type="checkbox"
                                      value=""
                                      id="nature1"
                                      @click=""
                                    />
                                    <label class="form-check-label" for="nature1">
                                      Immunosuppress
                                    </label>
                                </div>
                                <div class="form-check">
                                    <input
                                      class="form-check-input"
                                      type="checkbox"
                                      value=""
                                      id="nature2"
                                      @click=""
                                    />
                                    <label class="form-check-label" for="nature2">
                                      Non- immunosuppress
                                    </label>
                                </div>
                              </td>
                            </tr>
                            <tr>
                              <th>Deskripsi Penyakit<br> <span style="font-style:italic;color: grey;font-size: smaller;">Disease Description</span> </th>
                              <td>:</td>
                              <td>
                                a)Etiology/aetiology
                                <textarea v-model="aetiology" rows="2" class="form-control"></textarea>
                                <br>
                                b)Cara transmisi/mode of transmission
                                <textarea v-model="mode_transmission" rows="2" class="form-control"></textarea>
                                <br>
                                c)Tanda Klinikal/clinical sign
                                <textarea v-model="clinical_sign" rows="2" class="form-control"></textarea>
                              </td>
                            </tr>
                            <tr>
                              <th>Negara Asal<br> <span style="font-style:italic;color: grey;font-size: smaller;">Country of Origin (Vaccine)- COO</span> </th>
                              <td>:</td>
                              <td> <input
                              class="form-control"
                              type="file"
                              id="formFileCountryOrigin" @change=""/></td>
                            </tr>
                            <tr>
                              <th>Salinan Lesen Pembuat atau sijil pendaftaran kilang pembuat di negara pembuat<br> <span style="font-style:italic;color: grey;font-size: smaller;">Copy of manufacturing license or registration certificate of the manufacturer in the country of origin</span> </th>
                              <td>:</td>
                              <td> <input
                              class="form-control"
                              type="file"
                              id="formFileManufacturingLicense" @change=""/></td>
                            </tr>
                            <tr>
                              <th>Sijil GMP Kilang Pembuat<br> <span style="font-style:italic;color: grey;font-size: smaller;">Certification of GMP for the manufacturer</span> </th>
                              <td>:</td>
                              <td> <input
                              class="form-control"
                              type="file"
                              id="formFileGmpCertification" @change=""/></td>
                            </tr>
                            <tr>
                              <th>Nama dan alamat marketing Authorization Holder (MAH)<br> <span style="font-style:italic;color: grey;font-size: smaller;">Name and address of Marketing Authorization Holder (MAH)</span> </th>
                              <td>:</td>
                              <td><textarea v-model="mah" rows="4" class="form-control"></textarea></td>
                            </tr>
                            <tr>
                              <th>Salinan surat attorney or authorization oleh kilang pembuat vaksin<br> <span style="font-style:italic;color: grey;font-size: smaller;">Copy of letter of attorney or authorization letter by the manufacturer to appoint Marketing Authorization Holder</span> </th>
                              <td>:</td>
                              <td> <input
                              class="form-control"
                              type="file"
                              id="formFileAttorneyLetter" @change=""/></td>
                            </tr>
                            <tr>
                              <th>Salinan sijil pendaftaran dan sijil penjualan vaksin dari negara pembuat<br> <span style="font-style:italic;color: grey;font-size: smaller;">Copy of registration certificate or free sale certificate of vaccine in country of origin</span> </th>
                              <td>:</td>
                              <td> <input
                              class="form-control"
                              type="file"
                              id="formFileRefistrationCertOrigin" @change=""/></td>
                            </tr>
                            <tr>
                              <th>Salinan sijil pendaftaran dari dua negara lain bagi vaksin yang ingin didaftarkan di Malaysia<br> <span style="font-style:italic;color: grey;font-size: smaller;">Copy of registration certificate of the intended vaccine in two other countries</span> </th>
                              <td>:</td>
                              <td> <input
                              class="form-control"
                              type="file"
                              id="formFileRefistrationCertOther" @change=""/></td>
                            </tr>
                            <tr>
                              <td colspan="3" style="color: black;font-weight: bold;">Seksyen B (Perincian Produk)/Section B (Product Particular)</td>
                            </tr>
                            <tr>
                              <th>Nama Vaksin<br> <span style="font-style:italic;color: grey;font-size: smaller;">Name of vaccine (trade / generic name)</span> </th>
                              <td>:</td>
                              <td><input type="text" v-model="vaccine_name_generic" class="form-control" style="width: 100%;"></td>
                            </tr>
                            <tr>
                              <th>Vaksin Teknologi<br> <span style="font-style:italic;color: grey;font-size: smaller;">Technology of Vaccine</span> </th>
                              <td>:</td>
                              <td>
                                a)Konvisional/Conventional
                                <input
                                  class="form-control"
                                  type="file"
                                  id="formFileConventional" @change=""/>
                                  <br>
                                  b)Recombinant - (subunit / DNA / vector/ Gene Deleted / Artificial Cell Membrane)
                                  <input
                                  class="form-control"
                                  type="file"
                                  id="formFileRecombinant" @change=""/>
                              </td>
                            </tr>
                          </tbody>
                        </table>
                        <br>
                        
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
                        aria-controls="collapseTwo">
                        BAHAGIAN II : MAKLUMAT BAHAN MULA (<span style="font-style:italic;color: grey;font-size: small;">PART II: STARTING MATERIAL INFORMATION </span>)
                      </button>
                    </h2>
                    <div
                      id="collapseTwo"
                      class="accordion-collapse collapse"
                      aria-labelledby="headingTwo"
                      data-bs-parent="#accordionExample">
                      <div class="accordion-body">
                        <table class="notes">
                          <tbody>
                            <tr>
                              <td colspan="3" style="color: black;font-weight: bold;">Seksyen A (Master Seeds )/Section A (Master Seeds )</td>
                            </tr>
                            <tr>
                              <th>Maklumat sejarah Bibit Induk<br> <span style="font-style:italic;color: grey;font-size: smaller;">Information about the Master seed & working seed history</span> </th>
                              <td style="width: 2%;">:</td>
                              <td>
                                a)Sejarah pemerolehan bibit induk/history of acquisition of master seed & working seed <br>-isolation passage history
                                <input
                                  class="form-control"
                                  type="file"
                                  id="formFileSeedHistory" @change=""/>
                                  <br>
                                  b)Perjanjian pemindahan bahan/Material Transfer Agreement /letter of transfer agreement
                                  <input
                                  class="form-control"
                                  type="file"
                                  id="formFileTransferAgreement" @change=""/>
                                  <br>
                                  c)Nama penuh pathotype/ serotype/ strain Full name of pathotype/ serotype/ strain
                                  <input
                                  class="form-control"
                                  type="file"
                                  id="formFileStrain" @change=""/>
                              </td>
                            </tr>
                            <tr>
                              <th>Maklumat identiti bibit induk<br> <span style="font-style:italic;color: grey;font-size: smaller;">Information about the Master seed identity</span> </th>
                              <td>:</td>
                              <td>
                                a)Prosedur tetap perlu dilampirkan/SOP must be provided
                                <input
                                  class="form-control"
                                  type="file"
                                  id="formFileSopIdentityMaster" @change=""/>
                                  <br>
                                  b)Keputusan (serologi/DNA sequencing/gen) Results (serology / DNA sequencing / gene)
                                  <br>Results (serology / DNA sequencing / gene)
                                  <input
                                  class="form-control"
                                  type="file"
                                  id="formFileResultIdentityMaster" @change=""/>
                                 
                              </td>
                            </tr>
                            <tr>
                              <th>Maklumat ketulenan bibit induk<br> <span style="font-style:italic;color: grey;font-size: smaller;">Information about the Master seed purity</span> </th>
                              <td>:</td>
                              <td>
                                a)Prosedur tetap perlu dilampirkan/SOP must be provided
                                <input
                                  class="form-control"
                                  type="file"
                                  id="formFileSopIdentityMaster" @change=""/>
                                  <br>
                                  b)Keputusan (serologi/DNA sequencing/gen) Results (serology / DNA sequencing / gene)<br>Results (serology / DNA sequencing / gene)
                                  <input
                                  class="form-control"
                                  type="file"
                                  id="formFileResultIdentityMaster" @change=""/> 
                              </td>
                            </tr>
                            <tr>
                              <th>Sistem Pengurusan Lot Bibit<br> <span style="font-style:italic;color: grey;font-size: smaller;">Establishment of Seed Lot System
<br> - SOP on production control,
<br>- preparation, working, and production of seed</span> </th>
                              <td>:</td>
                              <td>
                                <input
                                  class="form-control"
                                  type="file"
                                  id="formFileSopLot" @change=""/>
                                  <br>
                                
                              </td>
                            </tr>
                            <tr>
                              <td colspan="3" style="color: black;font-weight: bold;">Seksyen B (Medium & Substrat)/Section B (Medium & Substrate)</td>
                            </tr>
                            <tr>
                              <th>Sila Senaraikan dan lampirkan COA<br> <span style="font-style:italic;color: grey;font-size: smaller;">-To provide list of media/substrate used with their origin (name of species if animal) with COA</span> </th>
                              <td>:</td>
                              <td>
                                <input
                                  class="form-control"
                                  type="file"
                                  id="formFileCoaAttachment" @change=""/>
                                  <br>
                                
                              </td>
                            </tr>
                            <tr>
                              <th>Media/Substrat untuk pengembangan bibit induk/bibit bekerja/bibit produksi<br> <span style="font-style:italic;color: grey;font-size: smaller;">Medium/ Substrate for Propagation of Vaccinal microrganisms (Master Seed/ Working Seed/ Production Seed, including Master Cell Stock information)<br>
                              i. SPF Egg or Tissue Culture ( Virus)<br>
                              ii. Media ( tissue culture & bacteria)<br>
                              iii. Others (Please specify), e.g., Live animal</span> </th>
                              <td>:</td>
                              <td>
                                <input
                                  class="form-control"
                                  type="file"
                                  id="formFileSubtractPropagation" @change=""/>
                                  </td>
                            </tr>
                            <tr>
                              <th>a) Status steril bagi telur SPF , sel kultur primer<br> <span style="font-style:italic;color: grey;font-size: smaller;">SPF status of production support (eggs, primary cell culture) *When master cell stock is not used</span><br>
                                <br>b) Lain-lain bahan pemula dari sumber haiwan<br> <span style="font-style:italic;color: grey;font-size: smaller;">Other starting material of animal origin *Part of culture media or freeze-drying excipient</span>
                              </th>
                              <td>:</td>
                              <td>
                                Sila Senaraikan & Lampirkan COA
                                <br>-To provide list of starting materials used (include name of species if animal) with COA
                                <input
                                  class="form-control"
                                  type="file"
                                  id="formFileCoa2" @change=""/>
                                  </td>
                            </tr>
                          </tbody>
                        </table>
                       
                      </div>
                    </div>
                  </div>
                  <!--  -->
                  <div class="accordion-item">
                    <h2 class="accordion-header" id="headingThree">
                      <button
                        class="accordion-button collapsed"
                        type="button"
                        data-bs-toggle="collapse"
                        data-bs-target="#collapseThree"
                        aria-expanded="false"
                        aria-controls="collapseThree">
                        BAHAGIAN III : PENGHASILAN DAN PENILAIAN VAKSIN (<span style="font-style:italic;color: grey;font-size: small;">PART III: VACCINES PRODUCTION & EVALUATION </span>)
                      </button>
                    </h2>
                    <div
                      id="collapseThree"
                      class="accordion-collapse collapse"
                      aria-labelledby="headingThree"
                      data-bs-parent="#accordionExample">
                      <div class="accordion-body">
                        <table class="notes">
                          <tbody>
                            <tr>
                              <td colspan="3" style="color: black;font-weight: bold;">Seksyen A (Kawalan Kualiti)/Section A (Quality Control)</td>
                            </tr>
                            <tr>
                              <th>Proses penghasilan vaksin<br> <span style="font-style:italic;color: grey;font-size: smaller;">Production outline/process flow</span> </th>
                              <td>:</td>
                              <td>
                                <input
                                  class="form-control"
                                  type="file"
                                  id="formFileProductionOutline" @change=""/>
                                  </td>
                            </tr>
                            <tr>
                              <th>Keadaan produk akhir<br> <span style="font-style:italic;color: grey;font-size: smaller;">Nature of final products</span> </th>
                              <td>:</td>
                              <td>
                                a) Type of vaccine
                                <div class="form-check">
                                    <input
                                      class="form-check-input"
                                      type="checkbox"
                                      value=""
                                      id="type1"
                                      @click=""
                                    />
                                    <label class="form-check-label" for="type1">
                                      Lived
                                    </label>
                                </div>
                                <div class="form-check">
                                    <input
                                      class="form-check-input"
                                      type="checkbox"
                                      value=""
                                      id="type2"
                                      @click=""
                                    />
                                    <label class="form-check-label" for="type2">
                                      Killed
                                    </label>
                                </div>
                                <br>
                                b) Number of strain
                                <div class="form-check">
                                    <input
                                      class="form-check-input"
                                      type="checkbox"
                                      value=""
                                      id="strain1"
                                      @click=""
                                    />
                                    <label class="form-check-label" for="strain1">
                                      Monovalent
                                    </label>
                                </div>
                                <div class="form-check">
                                    <input
                                      class="form-check-input"
                                      type="checkbox"
                                      value=""
                                      id="strain2"
                                      @click=""
                                    />
                                    <label class="form-check-label" for="strain2">
                                      Multivalent
                                    </label>
                                </div>
                                c) Form
                                <div class="form-check">
                                    <input
                                      class="form-check-input"
                                      type="checkbox"
                                      value=""
                                      id="form11"
                                      @click=""
                                    />
                                    <label class="form-check-label" for="form1">
                                      Lyophilised
                                    </label>
                                </div>
                                <div class="form-check">
                                    <input
                                      class="form-check-input"
                                      type="checkbox"
                                      value=""
                                      id="form2"
                                      @click=""
                                    />
                                    <label class="form-check-label" for="form2">
                                      frozen
                                    </label>
                                </div>
                              </td>
                            </tr>
                          </tbody>
                        </table>

                      </div>
                      <br>
                        <div class="d-flex">
                        <div  class="btn-right">
                          <button type="submit" @click="" class="btn btn-warning btn-text">
                            <i class="fa fa-save"></i> Simpan Draft
                          </button>
                          </div>
                        </div>
                    </div>
                  </div>
                  <!--  -->
                  <div class="accordion-item">
                    <h2 class="accordion-header" id="headingFour">
                      <button
                        class="accordion-button collapsed"
                        type="button"
                        data-bs-toggle="collapse"
                        data-bs-target="#collapseFour"
                        aria-expanded="false"
                        aria-controls="collapseFour"
                      >
                      BAHAGIAN IV: PRODUK SIAP (<span style="font-style:italic;color: grey;font-size: small;">PART IV: FINISHED PRODUCT </span>)
                      </button>
                    </h2>
                    <div
                      id="collapseFour"
                      class="accordion-collapse collapse"
                      aria-labelledby="headingFour"
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
                      <br>
                        <div class="d-flex">
                        <div  class="btn-right">
                          <button type="submit" @click="" class="btn btn-warning btn-text">
                            <i class="fa fa-save"></i> Simpan Draft
                          </button>
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
                      ><i class="fa fa-arrow-alt-to-left"></i> Kembali
                    </button>
                    <div  class="btn-right">
                      <button type="submit" @click="" class="btn btn-warning btn-text">
                            <i class="fa fa-save"></i> Simpan Draf
                          </button>
                    <button type="submit" @click="" class="btn btn-warning btn-text ml-auto">
                      <i class="fa fa-paper-plane"></i> Hantar Permohonan
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
  