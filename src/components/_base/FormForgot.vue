<template>
  <div>
    <b-container>
      <div
        class="d-flex justify-content-center"
        style="padding:30px;margin-top:50px"
      >
        <div class="align-self-center" style="font-weight:bold;font-size:20px">
          <img
            src="../../assets/img/coffee-logo.png"
            alt=""
            style="margin-right:10px"
          />Coffeeland
        </div>
      </div>
      <div class="padding-forgot">
        <h1 class="font-sm" style="text-align:center;font-weight:bold">
          Forgot your password?
        </h1>
        <br />
        <h4 class="font-sm2" style="margin-bottom:100px;text-align:center">
          Don’t worry, we got your back!
        </h4>
        <b-form @submit.prevent="sendMail">
          <b-form-input
            type="email"
            class="input"
            autocomplete="off"
            placeholder="Enter your email address to get link"
            required
            v-model="email"
          ></b-form-input
          ><br />
          <b-button
            block
            class="btn-style2 shadow"
            style="background-color:#FFBA33;color:#7D4F2A"
            type="submit"
            >Send</b-button
          >
          <h6
            style="margin-bottom:40px;margin-top:40px;text-align:center"
            v-if="sendNotif === 1"
          >
            <b-icon
              icon="circle-fill"
              animation="throb"
              font-scale="1"
            ></b-icon>
            Sending , Please Wait . . .
          </h6>
          <h6
            style="margin-bottom:40px;margin-top:40px;text-align:center"
            v-if="sendNotif === 2"
          >
            <b-icon
              icon="arrow-clockwise"
              animation="spin"
              font-scale="1"
            ></b-icon>
            Failed send link reset password, Please try again or Check your
            email
          </h6>
          <h6 style="margin-bottom:40px;margin-top:40px;text-align:center">
            Click Resend Link if you didn’t receive any link in 2 minutes
          </h6>
          <b-button
            block
            class="btn-style2 shadow"
            style="color:white;background-color:#6A4029"
            type="submit"
            >Resend Link</b-button
          ><br />
        </b-form>
        <b-button
          block
          class="btn-style2 shadow"
          style="color:white;background-color:#6A4029"
          @click="setPage('signin')"
          >Login here</b-button
        ><br />
      </div>
    </b-container>
  </div>
</template>

<script>
import { mapActions, mapMutations } from 'vuex'
import alertMixin from '../../mixins/alertMixin.js'
export default {
  name: 'Forgot',
  mixins: [alertMixin],
  data() {
    return {
      email: '',
      sendNotif: 0
    }
  },
  methods: {
    ...mapActions(['forgotPass']),
    ...mapMutations(['setPage']),
    sendMail() {
      this.sendNotif = 1
      const dataMail = {
        email: this.email
      }
      this.forgotPass(dataMail)
        .then(result => {
          this.sendNotif = 0
          this.makeToast('Done', `${result.data.msg}`, 'success')
        })
        .catch(error => {
          this.sendNotif = 2
          this.makeToast('Failed', `${error.data.msg}`, 'danger')
        })
    }
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;700;900&family=Rubik:wght@300;400;500;600;700&display=swap');
.rubik {
  font-family: 'Rubik', sans-serif;
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
.padding-forgot {
  padding: 80px;
  margin-top: 50px;
}
@media only screen and (max-width: 600px) {
  .padding-forgot {
    padding: 30px;
    margin-top: 10px;
  }
  .font-sm {
    font-size: 25px;
  }
  .font-sm2 {
    font-size: 20px;
  }
}
</style>
