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
                                <td>{{ this.applicant_name }}</td>
                              </tr>
                              <tr>
                                <th>Nombor Kad Pengenalan<br> <span style="font-style:italic;color: grey;font-size: smaller;">Identification Card (IC) Number of Applicant</span></th>
                                <td>:</td>
                                <td>{{ this.applicant_nric }}</td>
                              </tr>
                              <tr>
                                <th>Alamat<br> <span style="font-style:italic;color: grey;font-size: smaller;">Address</span> </th>
                                <td>:</td>
                                <td>{{ this.address1 }} {{ this.address2 }} {{ this.postcode }} {{ this.city }} {{ this.state }}</td>
                              </tr>
                              <tr>
                                <th>Nama Pengilang Vaksin<br> <span style="font-style:italic;color: grey;font-size: smaller;">Name of Vaccine Manufacturer</span> </th>
                                <td>:</td>
                                <td>{{ this.manufacturer_name }}</td>
                              </tr>
                              <tr>
                                <th>Nombor Pendaftaran Pengilang Vaksin Yang telah didaftarkan oleh DVS<br> <span style="font-style:italic;color: grey;font-size: smaller;">DVS Manufacturer Registration Number</span> </th>
                                <td>:</td>
                                <td>{{ this.dvs_manufacturer }}</td>
                              </tr>
                              <tr>
                                <th>Nama Vaksin<br> <span style="font-style:italic;color: grey;font-size: smaller;">Name of Vaccine</span> </th>
                                <td>:</td>
                                <td><input type="text" v-model="vaccine_name" class="form-control" style="width: 100%;" disabled></td>
                              </tr>
                              <tr>
                                <th>Penyakit yang disasarkan<br> <span style="font-style:italic;color: grey;font-size: smaller;">Target Disease</span> </th>
                                <td>:</td>
                                <td><textarea v-model="target_disease" rows="2" class="form-control" disabled></textarea></td>
                              </tr>
                              <tr>
                                <th>Spesies yang disasarkan<br> <span style="font-style:italic;color: grey;font-size: smaller;">Target Species</span> </th>
                                <td>:</td>
                                <td><textarea v-model="target_species" rows="2" class="form-control" disabled></textarea></td>
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
                                        disabled
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
                                        disabled
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
                                  <textarea v-model="aetiology" rows="2" class="form-control" disabled></textarea>
                                  <br>
                                  b)Cara transmisi/mode of transmission
                                  <textarea v-model="mode_transmission" rows="2" class="form-control" disabled></textarea>
                                  <br>
                                  c)Tanda Klinikal/clinical sign
                                  <textarea v-model="clinical_sign" rows="2" class="form-control" disabled></textarea>
                                </td>
                              </tr>
                              <tr>
                                <th>Negara Asal<br> <span style="font-style:italic;color: grey;font-size: smaller;">Country of Origin (Vaccine)- COO</span> </th>
                                <td>:</td>
                                <td> <input
                                class="form-control"
                                type="file"
                                id="formFileCountryOrigin" @change="" disabled/></td>
                              </tr>
                              <tr>
                                <th>Salinan Lesen Pembuat atau sijil pendaftaran kilang pembuat di negara pembuat<br> <span style="font-style:italic;color: grey;font-size: smaller;">Copy of manufacturing license or registration certificate of the manufacturer in the country of origin</span> </th>
                                <td>:</td>
                                <td> <input
                                class="form-control"
                                type="file"
                                id="formFileManufacturingLicense" @change="" disabled/></td>
                              </tr>
                              <tr>
                                <th>Sijil GMP Kilang Pembuat<br> <span style="font-style:italic;color: grey;font-size: smaller;">Certification of GMP for the manufacturer</span> </th>
                                <td>:</td>
                                <td> <input
                                class="form-control"
                                type="file"
                                id="formFileGmpCertification" @change="" disabled/></td>
                              </tr>
                              <tr>
                                <th>Nama dan alamat marketing Authorization Holder (MAH)<br> <span style="font-style:italic;color: grey;font-size: smaller;">Name and address of Marketing Authorization Holder (MAH)</span> </th>
                                <td>:</td>
                                <td><textarea v-model="mah" rows="4" class="form-control" disabled></textarea></td>
                              </tr>
                              <tr>
                                <th>Salinan surat attorney or authorization oleh kilang pembuat vaksin<br> <span style="font-style:italic;color: grey;font-size: smaller;">Copy of letter of attorney or authorization letter by the manufacturer to appoint Marketing Authorization Holder</span> </th>
                                <td>:</td>
                                <td> <input
                                class="form-control"
                                type="file"
                                id="formFileAttorneyLetter" @change="" disabled/></td>
                              </tr>
                              <tr>
                                <th>Salinan sijil pendaftaran dan sijil penjualan vaksin dari negara pembuat<br> <span style="font-style:italic;color: grey;font-size: smaller;">Copy of registration certificate or free sale certificate of vaccine in country of origin</span> </th>
                                <td>:</td>
                                <td> <input
                                class="form-control"
                                type="file"
                                id="formFileRefistrationCertOrigin" @change="" disabled/></td>
                              </tr>
                              <tr>
                                <th>Salinan sijil pendaftaran dari dua negara lain bagi vaksin yang ingin didaftarkan di Malaysia<br> <span style="font-style:italic;color: grey;font-size: smaller;">Copy of registration certificate of the intended vaccine in two other countries</span> </th>
                                <td>:</td>
                                <td> <input
                                class="form-control"
                                type="file"
                                id="formFileRefistrationCertOther" @change="" disabled/></td>
                              </tr>
                              <tr>
                                <td colspan="3" style="color: black;font-weight: bold;">Seksyen B (Perincian Produk)/Section B (Product Particular)</td>
                              </tr>
                              <tr>
                                <th>Nama Vaksin<br> <span style="font-style:italic;color: grey;font-size: smaller;">Name of vaccine (trade / generic name)</span> </th>
                                <td>:</td>
                                <td><input type="text" v-model="vaccine_name_generic" class="form-control" style="width: 100%;" disabled></td>
                              </tr>
                              <tr>
                                <th>Vaksin Teknologi<br> <span style="font-style:italic;color: grey;font-size: smaller;">Technology of Vaccine</span> </th>
                                <td>:</td>
                                <td>
                                  a)Konvisional/Conventional
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileConventional" @change="" disabled/>
                                    <br>
                                    b)Recombinant - (subunit / DNA / vector/ Gene Deleted / Artificial Cell Membrane)
                                    <input
                                    class="form-control"
                                    type="file"
                                    id="formFileRecombinant" @change="" disabled/>
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
                                    id="formFileSeedHistory" @change="" disabled/>
                                    <br>
                                    b)Perjanjian pemindahan bahan/Material Transfer Agreement /letter of transfer agreement
                                    <input
                                    class="form-control"
                                    type="file"
                                    id="formFileTransferAgreement" @change="" disabled/>
                                    <br>
                                    c)Nama penuh pathotype/ serotype/ strain Full name of pathotype/ serotype/ strain
                                    <input
                                    class="form-control"
                                    type="file"
                                    id="formFileStrain" @change="" disabled/>
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
                                    id="formFileSopIdentityMaster" @change="" disabled/>
                                    <br>
                                    b)Keputusan (serologi/DNA sequencing/gen) Results (serology / DNA sequencing / gene)
                                    <br>Results (serology / DNA sequencing / gene)
                                    <input
                                    class="form-control"
                                    type="file"
                                    id="formFileResultIdentityMaster" @change="" disabled/>

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
                                    id="formFileSopIdentityMaster" @change="" disabled/>
                                    <br>
                                    b)Keputusan (serologi/DNA sequencing/gen) Results (serology / DNA sequencing / gene)<br>Results (serology / DNA sequencing / gene)
                                    <input
                                    class="form-control"
                                    type="file"
                                    id="formFileResultIdentityMaster" @change="" disabled/>
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
                                    id="formFileSopLot" @change="" disabled/>
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
                                    id="formFileCoaAttachment" @change="" disabled/>
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
                                    id="formFileSubtractPropagation" @change="" disabled/>
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
                                    id="formFileCoa2" @change="" disabled/>
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
                                    id="formFileProductionOutline" @change="" disabled/>
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
                                        disabled
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
                                        disabled
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
                                        disabled
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
                                        disabled
                                      />
                                      <label class="form-check-label" for="strain2">
                                        Multivalent
                                      </label>
                                  </div>
                                  <br>
                                  c) Form
                                  <div class="form-check">
                                      <input
                                        class="form-check-input"
                                        type="checkbox"
                                        value=""
                                        id="form11"
                                        @click=""
                                        disabled
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
                                        disabled
                                      />
                                      <label class="form-check-label" for="form2">
                                        Frozen
                                      </label>
                                  </div>
                                  <div class="form-check">
                                      <input
                                        class="form-check-input"
                                        type="checkbox"
                                        value=""
                                        id="form3"
                                        @click=""
                                        disabled
                                      />
                                      <label class="form-check-label" for="form2">
                                        Emulsion
                                      </label>
                                  </div>
                                  <div class="form-check">
                                      <input
                                        class="form-check-input"
                                        type="checkbox"
                                        value=""
                                        id="form4"
                                        @click=""
                                        disabled
                                      />
                                      <label class="form-check-label" for="form2">
                                        Suspension
                                      </label>
                                  </div>
                                  <br>
                                  d) Technology of Vaccine
                                  <div class="form-check">
                                      <input
                                        class="form-check-input"
                                        type="checkbox"
                                        value=""
                                        id="vaccine1"
                                        @click=""
                                        disabled
                                      />
                                      <label class="form-check-label" for="form1">
                                        Whole Cell Vaccine
                                      </label>
                                  </div>
                                  <div class="form-check">
                                      <input
                                        class="form-check-input"
                                        type="checkbox"
                                        value=""
                                        id="vaccine1"
                                        @click=""
                                        disabled
                                      />
                                      <label class="form-check-label" for="form1">
                                        Recombinant Vaccine
                                      </label>
                                  </div>
                                      <div class="form-check">
                                      <input
                                        class="form-check-input"
                                        type="checkbox"
                                        value=""
                                        id="vaccine1"
                                        @click=""
                                        disabled
                                      />
                                      <label class="form-check-label" for="form1">
                                        Virus Vector Vaccine
                                      </label>
                                  </div>
                                  <div class="form-check">
                                      <input
                                        class="form-check-input"
                                        type="checkbox"
                                        value=""
                                        id="vaccine1"
                                        @click=""
                                        disabled
                                      />
                                      <label class="form-check-label" for="form1">
                                        DNA Vaccine
                                      </label>
                                  </div>
                                  <div class="form-check">
                                      <input
                                        class="form-check-input"
                                        type="checkbox"
                                        value=""
                                        id="vaccine1"
                                        @click=""
                                        disabled
                                      />
                                      <label class="form-check-label" for="form1">
                                        Subunit Vaccine
                                      </label>
                                  </div>
                                  <div class="form-check">
                                      <input
                                        class="form-check-input"
                                        type="checkbox"
                                        value=""
                                        id="vaccine1"
                                        @click=""
                                        disabled
                                      />
                                      <label class="form-check-label" for="form1">
                                        Peptide Vaccine
                                      </label>
                                  </div>
                                </td>
                              </tr>
                              <tr>
                                <th>Salinan sijil perlepasan untuk 3 batch terkini<br> <span style="font-style:italic;color: grey;font-size: smaller;">Copy of assay certificate or certificate of release for
  latest 3 consecutive batches.
  </span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan
                                  <br>-Please Attach
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th> Komposisi Kimia<br> <span style="font-style:italic;color: grey;font-size: smaller;">Chemical compositions & safety test (chemical starting materials used as adjuvant/stabilizer/preservative)</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Senaraikan
                                  <br>-Please list of chemical used and safety report
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th> Kandungan kelembapan<br><span style="font-style:italic;color: grey;font-size: smaller;">Moisture contents (for Lyophilised vaccine)</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan SOP & COA
                                  <br>-Please Attach written SOP & COA
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th> Vakum <br><span style="font-style:italic;color: grey;font-size: smaller;">Vacuum (for Lyophilised vaccine)</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan SOP & COA
                                  <br>-Please Attach written SOP & COA
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th> Kestabilan emulsi <br><span style="font-style:italic;color: grey;font-size: smaller;">Emulsion stability ( if applicable)</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan SOP & COA
                                  <br>-Please Attach written SOP & COA
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th> Kelikatan Vaksin <br><span style="font-style:italic;color: grey;font-size: smaller;">Viscosity of vaccine (if applicable)</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan SOP & COA
                                  <br>-Please Attach written SOP & COA
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                               <tr>
                              <th> Pengujian ketulenan <br><span style="font-style:italic;color: grey;font-size: smaller;">Purity test (for live vaccines)</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan SOP & COA
                                  <br>-Please Attach written SOP & COA
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th> Pengujian steril (QC) <br><span style="font-style:italic;color: grey;font-size: smaller;">Sterility tests (QC)</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan SOP & COA
                                  <br>-Please Attach written SOP & COA
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                                <td colspan="3" style="color: black;font-weight: bold;">Seksyen B (Keselamatan)/Section B (Safety)</td>
                              </tr>
                              <tr>
                              <th> Komposisi produk akhir <br><span style="font-style:italic;color: grey;font-size: smaller;">Composition of the final product (vaccine and diluent)
                                <br>-levels of toxic components
                                <br>-list of each component in FP packaging</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan
                                  <br>-Please Attach
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th>  Keselamatan Vaksin <br><span style="font-style:italic;color: grey;font-size: smaller;">Vaccine Safety</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan
                                  <br>-Please Attach written SOP with safety report
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th>  Pengujian innocuiti <br><span style="font-style:italic;color: grey;font-size: smaller;">Innocuity tests</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan
                                  <br>-Please Attach written SOP with test result
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th> Proses melemahkan vaksin<br><span style="font-style:italic;color: grey;font-size: smaller;">Vaccine Attenuation process (for live/ attenuated vaccine)</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan
                                  <br>-Please Attach written SOP with test result
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th>Pengembalian kepada virulensi (LV) / kajian back passage<br><span style="font-style:italic;color: grey;font-size: smaller;">Reversion to virulence (LV) / back passage study</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan
                                  <br>-Please Attach written SOP with test result
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th>Proses penyahaktifan vaksin<br><span style="font-style:italic;color: grey;font-size: smaller;">Vaccine inactivation process (for killed vaccine/inactivated antigens)</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan
                                  <br>-Please Attach written SOP with test result
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th>Penentuan margin keselamatan kinetik penyahaktifan<br><span style="font-style:italic;color: grey;font-size: smaller;">Inactivation kinetic safety margin determination</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan
                                  <br>-Please Attach written SOP with test result
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th>Pengujian immunosupresi<br><span style="font-style:italic;color: grey;font-size: smaller;">Immunosuppression Test (if applicable)</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan
                                  <br>-Please Attach written SOP with test result
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th>Pengujian inaktif residu<br><span style="font-style:italic;color: grey;font-size: smaller;">Residual inactivant test (for killed+live vaccine)</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan
                                  <br>-Please Attach written SOP with test result
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                                <td colspan="3" style="color: black;font-weight: bold;">Seksyen C (Efikasi) /Section B (Efficacy) </td>
                              </tr>
                              <tr>
                              <th>Potency /Challenge test <br><span style="font-style:italic;color: grey;font-size: smaller;">Potency (Efficacy) </span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan
                                  <br>-Please Attach written SOP with report/technical data
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th>Ujian imunogenisiti <br><span style="font-style:italic;color: grey;font-size: smaller;">Immunogenicity test</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan
                                  <br>-Please Attach written SOP with report/technical data
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th>Ujian imunogenisiti <br><span style="font-style:italic;color: grey;font-size: smaller;">Immunogenicity test</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan
                                  <br>-Please Attach written SOP with report/technical data
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th>Dos imunogenik minimum<br><span style="font-style:italic;color: grey;font-size: smaller;">Minimum immunogenic dose (Procedure for determination minimum dose (MID) / Probit analysis)</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan
                                  <br>-Please Attach written SOP with report/technical data
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th>Kajian lapangan<br><span style="font-style:italic;color: grey;font-size: smaller;">Field trials <br>-Field trials are conducted in 3 farms in different (3) locations with complete address </span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan
                                  <br>-Please Attach study report with technical data
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th>Tahap Imun dan tempoh di dalam hos<br><span style="font-style:italic;color: grey;font-size: smaller;">Immune level and duration in intended host</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan
                                  <br>-Please Attach written SOP with report/technical data
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th>Tahap Imun dan tempoh di dalam progeny<br><span style="font-style:italic;color: grey;font-size: smaller;">Immune level and duration in progeny (maternal derived antibody-passive immunity) if applicable</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan
                                  <br>-Please Attach written SOP with report/technical data
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th>Pengujian kestabilan<br><span style="font-style:italic;color: grey;font-size: smaller;">Stability test</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan
                                  <br>-Please Attach written SOP with report/technical data
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th>Jangka hayat<br><span style="font-style:italic;color: grey;font-size: smaller;">Shelf life </span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan
                                  <br>-Please Attach
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                            </tbody>
                          </table>

                        </div>
                        <br>

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
                       <table class="notes">
                        <tbody>
                              <tr>
                                <td colspan="3" style="color: black;font-weight: bold;">Seksyen A (Rejim Vaksinasi)/Seksyen A (Rejim Vaksinasi)</td>
                              </tr>
                              <tr>
                              <th>Risiko meggunakan vaksin bergantung kepada strain atau teknologi pembuatan vaksin<br><span style="font-style:italic;color: grey;font-size: smaller;">Risk of application of the vaccine based on strain used or type of manufacturing technology (Category II &III of Biotech vaccine) <br>- Safe to host, human or environment </span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan
                                  <br>-Please Attach
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th>Jadual pemvaksinan<br><span style="font-style:italic;color: grey;font-size: smaller;">Vaccinating schedule</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan
                                  <br>-Please Attach
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th>Kumpulan sasaran<br><span style="font-style:italic;color: grey;font-size: smaller;">Target age/group</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan
                                  <br>-Please Attach
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th>Pencair<br><span style="font-style:italic;color: grey;font-size: smaller;">Diluent  <br>- Name of diluent </span> </th>
                                <td>:</td>
                                <td>
                                  Sila Nyatakan dan Lampirkan COA
                                  <br>-Please specify & attach COA
                                 <input type="text" v-model="diluent" class="form-control" style="width: 100%;" disabled><br>
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th>Dos dan cara pemvaksinan<br><span style="font-style:italic;color: grey;font-size: smaller;">Dosage and route of vaccination</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan
                                  <br>-Please Attach
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                                <td colspan="3" style="color: black;font-weight: bold;">Seksyen B (Maklumat Pembungkusan)/Section B (Packaging Information)</td>
                              </tr>
                              <tr>
                                <th>Maklumat Asas<br> <span style="font-style:italic;color: grey;font-size: smaller;">General information</span> </th>
                                <td>:</td>
                                <td>
                                  a. Isi isipadu/berat bekas<br><span style="font-style:italic;color: grey;font-size: smaller;">Fill volume/ weight of container </span>
                                  <input type="text" v-model="diluent" rows="2" class="form-control" disabled>
                                  <br>
                                  b. Jenis bekas<br><span style="font-style:italic;color: grey;font-size: smaller;">Type of container</span>
                                  <input type="text" v-model="diluent" rows="2" class="form-control" disabled>
                                  <br>
                                  c. Bahan yang digunakan bagi bekas primer<br><span style="font-style:italic;color: grey;font-size: smaller;">Material of the primary container</span>
                                  <input type="text" v-model="diluent" rows="2" class="form-control" disabled><br>
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    <br>
                                  d. Jenis dan bahan penyumbat<br><span style="font-style:italic;color: grey;font-size: smaller;">Type and material of stopper</span>
                                  <input type="text" v-model="diluent" rows="2" class="form-control" disabled><br>
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    <br>
                                </td>
                              </tr>
                              <tr>
                              <th>Maklumat label dan risalah<br><span style="font-style:italic;color: grey;font-size: smaller;">Label information (all below information shall available on the product’s label and  pamphlet)<br></span>
                              a. Nama Produk<br><span style="font-style:italic;color: grey;font-size: smaller;">Product Name<br></span>
                              b. Strain<br><span style="font-style:italic;color: grey;font-size: smaller;">Strain<br></span>
                              c. Dos setiap pakej <br><span style="font-style:italic;color: grey;font-size: smaller;">Doses per package<br></span>
                              d. Maklumat pengeluar<br><span style="font-style:italic;color: grey;font-size: smaller;">Manufactured by<br></span>
                              e. No. batch/siri , tarikh pembuatan dan tamat tempoh<br><span style="font-style:italic;color: grey;font-size: smaller;">Batch/serial number, manufacturing and expiry date<br></span>
                              f. Spesis yang disasarkan<br><span style="font-style:italic;color: grey;font-size: smaller;">Target sepsis<br></span>
                              g. Syarat penyimpanan<br><span style="font-style:italic;color: grey;font-size: smaller;">Storage condition<br></span>
                              h. *Indikasi dan kontraindikasi<br><span style="font-style:italic;color: grey;font-size: smaller;">Indications and contra-indications<br></span>
                              i. *Kesan sampingan dan langkah berjaga-jaga<br><span style="font-style:italic;color: grey;font-size: smaller;">Side effects and precautions (human & animals<br></span></th>
                                <td>:</td>
                                <td>
                                  a. Label asal/sebenar
                                  <br>-Original label
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    <br>b. Label dicetak
                                    <br>-Printed label
                                    <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    <br>c. Risalah
                                    <br>-Pamphlet
                                    <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <tr>
                              <th>Gambar produk <br>(dengan pembungkusan berbeza –jika ada)<br><span style="font-style:italic;color: grey;font-size: smaller;">Photo of product ( with different packaging – if available)</span> </th>
                                <td>:</td>
                                <td>
                                  Sila Lampirkan maklumat berkenaan  (Muat naik)
                                  <br>-Please Attach (Upload)
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                    </td>
                              </tr>
                              <br>
                              <tr>
                                <td colspan="3" style="color: black;font-weight: bold;">Seksyen C (Dokumen Sokongan & Maklumat Lain)/Section C (Other Information & Supporting Documents)</td>
                              </tr>
                              <tr>
                                <th>Pilih & Sila Lampirkan maklumat berkenaan<br>(dengan pembungkusan berbeza –jika ada)<br><span style="font-style:italic;color: grey;font-size: smaller;">Choose any and Attach File</span> </th>
                                  <td>: </td>
                                  <td>
                                  <div class="form-check">
                                      <input
                                        class="form-check-input"
                                        type="checkbox"
                                        value=""
                                        id="type1"
                                        @click="" disabled
                                      />
                                      <label class="form-check-label" for="type1">
                                        Pharmacopeia
                                      </label>
                                  </div>
                                  <div class="form-check">
                                      <input
                                        class="form-check-input"
                                        type="checkbox"
                                        value=""
                                        id="type1"
                                        @click="" disabled
                                      />
                                      <label class="form-check-label" for="type1">
                                        ASEAN Standard
                                      </label>
                                  </div>
                                  <div class="form-check">
                                      <input
                                        class="form-check-input"
                                        type="checkbox"
                                        value=""
                                        id="type1"
                                        @click="" disabled
                                      />
                                      <label class="form-check-label" for="type1">
                                        VICH (Veterinary International Cooperation on <br>Harmonization of Technical Requirement for <br>Registration of Veterinary Medicinal Products)
                                      </label>
                                  </div>
                                  <div class="form-check">
                                      <input
                                        class="form-check-input"
                                        type="checkbox"
                                        value=""
                                        id="type1"
                                        @click="" disabled
                                      />
                                      <label class="form-check-label" for="type1">
                                        OIE
                                      </label>
                                  </div>
                                  <div class="form-check">
                                      <input
                                        class="form-check-input"
                                        type="checkbox"
                                        value=""
                                        id="type1"
                                        @click="" disabled
                                      />
                                      <label class="form-check-label" for="type1">
                                        Journal
                                      </label>
                                  </div>
                                  <input
                                    class="form-control"
                                    type="file"
                                    id="formFileProductionOutline" @change="" disabled/>
                                  </td>

                              </tr>
                        </tbody>
                       </table>
                      </div>
                        <br>
                      </div>
                    </div>
                    <!--  -->
                  </div>
                         <br><br>
                  <div class="d-flex">
                      <button
                        @click="back"
                        class="btn btn-primary btn-text"
                        ><i class="fa fa-arrow-alt-to-left"></i> Kembali
                      </button>
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
    import Swal from 'sweetalert2';
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
                applicant_name: "",
                applicant_nric: "",
                address1: "",
                address2: "",
                postcode: "",
                state: "",
                city: "",
                manufacturer_name: "",
                dvs_manufacturer: "",
                vaccine_name:"",
                target_disease:"",
                target_species:"",
                Id:""
            };
        },
        beforeMount() {
            this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
            this.getList();
            let urlParams = new URLSearchParams(window.location.search);
            this.Id = urlParams.get("id");

        },
        mounted(){
          this.getVacInfoList();
        },

        methods: {
          async getList(){
            const headers = {
              Authorization: "Bearer " + this.userdetails.access_token,
              Accept: "application/json",
              "Content-Type": "application/json",
            };
            const response = await this.$axios.post(
              "staff-management/getUserListByEmail",
              { email: this.userdetails.user.email},
              {
                headers,
              }
            );
            if (response.data.code == 200 || response.data.code == "200") {
              this.applicant_name = response.data.list[0].name;
              this.applicant_nric = response.data.list[0].nric_no;
              this.address1 = response.data.list[0].address_1;
              this.address2 =response.data.list[0].address_2;
              this.postcode =response.data.list[0].poscode;
              this.state = response.data.list[0].state;
              this.city = response.data.list[0].city;
              this.manufacturer_name = response.data.list[0].name_vacs_manufacturer;
              this.dvs_manufacturer = response.data.list[0].reg_num_vacs_manufacturer;

            } else {
              window.alert("no data");
            }
          },

          async getVacInfoList(){
            const headers = {
              Authorization: "Bearer " + this.userdetails.access_token,
              Accept: "application/json",
              "Content-Type": "application/json",
            };

            const response = await this.$axios.post(
              "vaccine-registration/getVacInfoList",
              {
                email: this.userdetails.user.email,
                id: this.Id
              },
              {
                headers,
              });

              if (response.data.code == 200 || response.data.code == "200"){
                this.vaccine_name = response.data.list[0].vac_name;
                this.target_disease = response.data.list[0].targetted_disease;
                this.target_species = response.data.list[0].targetted_species;
              }

          },

          async onDraft(){
            const headers = {
              Authorization: "Bearer " + this.userdetails.access_token,
              Accept: "application/json",
              "Content-Type": "application/json",
            };
            const response = await this.$axios.post(
              "vaccine-registration/regDraft",
              {
                email: this.userdetails.user.email,
                applicant_name: this.applicant_name,
                applicant_nric: this.applicant_nric,
                address1: this.address1,
                address2: this.address2,
                postcode: this.postcode,
                state: this.state,
                city: this.city,
                manufacturer_name: this.manufacturer_name,
                vaccine_name: this.vaccine_name,
                target_disease: this.target_disease,
                target_species: this.target_species,
              },
              {
                headers,
              }
            );
            if (response.data.code == 200 || response.data.code == "200") {
                await this.$swal.fire(
                                  'Berjaya Disimpan Sebagai Draf!',
                                  '',
                                  'success',
                                );
                this.$router.push("/Modules/Vaccine/vaccine-list");
            } else {
               this.$swal.fire({
                              icon: 'error',
                              title: 'Oops... Something Went Wrong!',
                              text: 'the error is: ' + JSON.stringify(response.data.message),
                            });
            }
          },

          async onSubmit(){
            const headers = {
              Authorization: "Bearer " + this.userdetails.access_token,
              Accept: "application/json",
              "Content-Type": "application/json",
            };
            const response = await this.$axios.post(
              "vaccine-registration/regSave",
              {
                email: this.userdetails.user.email,
                applicant_name: this.applicant_name,
                applicant_nric: this.applicant_nric,
                address1: this.address1,
                address2: this.address2,
                postcode: this.postcode,
                state: this.state,
                city: this.city,
                manufacturer_name: this.manufacturer_name,
                vaccine_name: this.vaccine_name,
                target_disease: this.target_disease,
                target_species: this.target_species,
              },
              {
                headers,
              }
            );
            if (response.data.code == 200 || response.data.code == "200") {
                await this.$swal.fire(
                                  'Permohonan Berjaya Dihantar!',
                                  '',
                                  'success',
                                );
                this.$router.push("/Modules/Vaccine/vaccine-list");
            } else {
               this.$swal.fire({
                              icon: 'error',
                              title: 'Oops... Something Went Wrong!',
                              text: 'the error is: ' + JSON.stringify(response.data.message),
                            });
            }
          },

          back(){
            this.$router.go(-1);
          }
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
  