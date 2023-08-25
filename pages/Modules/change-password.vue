<template>
  
     <div id="layoutSidenav">
      <CommonSidebar />
      <div id="layoutSidenav_content">
        <CommonHeader />
    <main>
    <div style="margin-right: auto; margin-left: auto ; margin-top:100px" class="row login-box">
      <img src="~/assets/images/logo-main1.png" />
      <div class="text mb-0">
        <h4>Tukar Kata Laluan</h4>
        <!-- <p>
          Enter your email address and we will send you a link to reset your
          password.
        </p> -->
      </div>

      <div class="mb-1">
        <label for="inputEmail">Kata Laluan Baharu</label>
        <input
          class="form-control"
          id="inputEmail"
          type="password"
          v-model="password"
        />
      </div>
      <div class="mb-1">
        <label for="inputEmail">Pengesahan Kata Laluan</label>
        <input
          class="form-control"
          id="inputEmail"
          type="password"
          v-model="Cnfpassword"
        />
      </div>
      <Error :message="emailerror" v-if="emailerror" />
      <div class="d-flex align-items-center mt-3 mb-2">
        <button style="margin-left: auto; margin-right: auto;" class="btn login-btn" @click="OnSubmit">Simpan</button>
      </div>
    </div>
     <div
      class="modal fade"
      id="password-change"
      tabindex="-1"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-dialog-centered modal-sm password-change">
        <div class="modal-content">
          <div class="modal-body">

            <p>Kata Laluan Berjaya Ditukar.</p>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary btn-ok"  v-on:click="redirectPage" data-bs-dismiss="modal">Ok</button>
          </div>
        </div>
      </div>
    </div>
    </main>
     </div>
    </div>
 
</template>
<script>
import CommonHeader from "../../components/CommonHeader.vue";
import CommonSidebar from "../../components/CommonSidebar.vue";
import Error from "~/components/Error";
import Loader from "../../components/loader.vue";
export default {
  components: { CommonSidebar, CommonHeader },
  name: "change-password",
  head: {
    script: [
      {
        src: "/app/js/bootstrap.bundle.min.js",
        body: true,
        crossorigin: "anonymous",
      },
      {
        src: "/app/js/scripts.js",
        body: true,
        crossorigin: "anonymous",
      },
    ],
  },
  data() {
    return {
      loader: false,
      userid: "",
      password: "",
      Cnfpassword: "",
      alphaNumeric: "",
      specialChar: "",
      settinglist: [],
      emailerror: null,
      minPwdError: null,
      maxPwdError: null,
      letterCaseError: null,
      alphaNumericError: null,
      specialCharError: null,
      validate: false,
    };
  },
  beforeMount() {
    this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
    console.log('my userdeatila',this.userdetails);
  },
  methods: {


    async OnSubmit() {
      this.emailerror = null;
      this.validate = true;
      try {
        if (!this.password) {
          this.emailerror = "Kata Laluan Adalah Diperlukan!";
        }
        if (this.password != this.Cnfpassword) {
          this.emailerror = "Pengesahan Kata Laluan Tidak Sah";
          this.validate = false;
        }
        if (this.password.length < 6) {
          this.emailerror = "Bilangan Abjad Tidak Mencukupi";
          this.validate = false;
        }
        if (this.password.length > 12) {
          this.emailerror = "Bilangan Abjad Telah Melebihi";
          this.validate = false;
        }

        if (this.password && this.validate) {
          this.loader = true;
          const response = await this.$axios.post("reset/changePassword", {
            userid: this.userdetails.user.id,
            password: this.password,
          });
          if (response.data.code == 200 || response.data.code == '200') {
            this.resetmodel();
            this.$nextTick(() => {
               $("#password-change").modal("show");
             });
          } else {
           this.loader = false;
            this.$swal.fire({
                  icon: 'error',
                  title: 'Oops... Something Went Wrong!',
                  text: 'the error is: ' + JSON.stringify(response.data.message),
                  footer: ''
                });
          }
        }
      } catch (e) {
        console.log("api not working", e);
        this.loader = false;
      }
    },
     resetmodel() {
      this.password = "";
      this.Cnfpassword = "";
    },

    redirectPage(){
      localStorage.removeItem('userdetails');
      this.$router.push("/staff-login");
    },
  }
};
</script>
