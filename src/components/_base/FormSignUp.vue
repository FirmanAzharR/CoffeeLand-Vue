<template>
  <div>
    <b-container class="">
      <div class="d-flex justify-content-between" style="padding:30px">
        <div class="align-self-center" style="font-weight:bold;font-size:20px">
          <img
            src="../../assets/img/coffee-logo.png"
            alt=""
            style="margin-right:10px"
          />Coffeeland
        </div>
        <div class="align-self-center">
          <b-button class="btn-style" @click="setPage('signin')"
            >Login</b-button
          >
        </div>
      </div>
      <div class="padding-signup">
        <h3
          style="text-align:center;color:#7d4f2a;margin-bottom:50px;font-weight:bold"
        >
          Sign Up
        </h3>
        <b-form @submit.prevent="onSubmit" @reset.prevent="onReset">
          <label for="" class="label-input">Email Address :</label>
          <b-form-input
            v-focus
            v-model="form.user_email"
            type="email"
            class="input"
            autocomplete="off"
            placeholder="Enter your email address"
            required
          ></b-form-input>
          <label for="" class="label-input">Password :</label>
          <b-form-input
            v-model="form.user_password"
            type="password"
            class="input"
            placeholder="Enter your password"
            autocomplete="current-password"
            required
          ></b-form-input>
          <label for="" class="label-input">Phone Number :</label>
          <b-form-input
            v-model="form.user_phone"
            type="number"
            class="input"
            placeholder="Enter your phone number"
            required
          ></b-form-input>
          <br />
          <b-button
            type="submit"
            block
            class="btn-style2 shadow"
            style="background-color:#FFBA33;color:#7D4F2A"
            >Sign Up</b-button
          ><br />
          <b-button
            block
            class="btn-style2 shadow"
            style="background-color:white;color:black
                "
            ><img
              src="../../assets/img/logo-google.png"
              alt=""
              style="margin-right:10px"
            />Sign Up with Google</b-button
          ><br />
          <h6
            for=""
            style="margin-top:40px;margin-bottom:40px;text-align:center"
          >
            Alredy have account ?
          </h6>
          <br />
          <b-button
            block
            class="btn-style2 shadow"
            style="color:white;background-color:#6A4029"
            @click="setPage('signin')"
            >Login here</b-button
          ><br />
        </b-form>
      </div>
    </b-container>
  </div>
</template>

<script>
import { mapActions, mapMutations } from 'vuex'

export default {
  name: 'SignUp',
  data() {
    return {
      form: {
        user_name: 'Default',
        user_email: '',
        user_phone: '',
        user_password: ''
      }
    }
  },
  methods: {
    ...mapActions(['signup']),
    ...mapMutations(['setPage']),
    makeToast(bodyMsg, msg, variant) {
      this.$bvToast.toast(bodyMsg, {
        title: msg,
        variant: variant,
        solid: true
      })
    },
    onSubmit() {
      this.signup(this.form)
        .then(result => {
          this.makeToast(
            'Congratulations',
            `Your account ${result.data.data.user_email} created successfully`,
            'success'
          )
          this.onReset()
        })
        .catch(error => {
          this.makeToast('Create account Failed', error.data.msg, 'danger')
        })
    },
    onReset() {
      this.form = {
        user_email: '',
        user_password: ''
      }
    }
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;700;900&family=Rubik:wght@300;400;500;600;700&display=swap');
.rubik {
  font-family: 'Rubik', sans-serif;
}
.padding-signup {
  padding: 80px;
  margin-top: 20px;
}
.responsive {
  width: 100%;
  height: auto;
}
.btn-style {
  padding: 10px;
  width: 120px;
  background-color: #ffba33;
  border-radius: 20px;
  color: #7d4f2a;
  font-weight: 600;
  border: none;
}
.btn-style2 {
  padding: 10px;
  height: 55px;
  border-radius: 20px;
  font-weight: 600;
  border: none;
}
.label-input {
  color: #868b95;
  font-weight: bold;
}
.input {
  height: 55px;
  border-radius: 20px;
  margin-bottom: 15px;
}
.input:focus {
  box-shadow: 0 0 0 0.2rem rgba(163, 100, 65, 0.25);
  border-color: #7d4f2a;
}
.shadow {
  -webkit-box-shadow: 1px 2px 8px 0px #2e2d2d54;
  -moz-box-shadow: 1px 2px 8px 0px #2e2d2d54;
  box-shadow: 1px 2px 8px 0px #2e2d2d54;
}
@media only screen and (max-width: 600px) {
  .padding-signup {
    padding: 30px;
    margin-top: 10px;
  }
}
</style>
