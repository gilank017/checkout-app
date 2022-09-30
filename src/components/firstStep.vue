<template>
  <div class="card card-checkout">
    <div class="row">
      <div class="col-md-9">
        <div class="header-step">
          <div class="title-step">Delivery Detail</div>
          <div class="form-check">
            <input class="form-check-input" type="checkbox" v-model="visibleDropshipper" id="dropshipperCheckbox" @change="handleTotal">
            <label class="form-check-label" for="dropshipperCheckbox">
              Send As Dropshipper
            </label>
          </div>
        </div>
        <div class="row">
          <div class="col-md-7">
            <div class="mb-3">
              <c-input label="Email" forId="forEmail" type="email" :className="errorInfoMessage.email.status" :message="errorInfoMessage.email.message" placeholder="Insert Email" v-model="infoForm.email" />
            </div>
            <div class="mb-3">
              <c-input label="Phone Number" forId="forPhone" type="number" :className="errorInfoMessage.phone.status" :message="errorInfoMessage.phone.message" placeholder="Insert Phone Number" v-model="infoForm.phone" />
            </div>
            <div class="mb-3">
              <c-text-area label="Delivery Address" forId="forAddress" placeholder="Insert Delivery Address" v-model="infoForm.address" />
            </div>
          </div>
          <div v-if="visibleDropshipper" class="col-md-5">
            <div class="mb-3">
              <c-input label="Dropshipper Name" forId="forDropshippername" :className="errorInfoMessage.dropshipperName.status" :message="errorInfoMessage.dropshipperName.message"  placeholder="Insert Dropshipper Name" v-model="infoForm.dropshipperName"/>
            </div>
            <div class="mb-3">
              <c-input label="Dropshipper Phone Number" forId="forPhoneNumber" type="number" :className="errorInfoMessage.dropshipperPhone.status" :message="errorInfoMessage.dropshipperPhone.message"  placeholder="Insert Dropshipper Phone Number" v-model="infoForm.dropshipperPhone" />
            </div>
          </div>
        </div>
      </div>
      <div class="col-md-3">
        <div class="border-summary px-4">
          <div class="summary-info">
            <div class="title-summary">Summary</div>
            <p class="items-summary">10 Items Purchased</p>
          </div>
          <div class="pricing-summary">
            <div class="pricing-description">
              <div class="d-flex justify-content-between">
                <p class="text-total m-0">Cost of goods</p>
                <p class="m-0"><strong>{{ totalGoods }}</strong></p>
              </div>
              <div v-if="visibleDropshipper" class="d-flex justify-content-between">
                <p class="text-total m-0">Dropshipping Fee</p>
                <p class="m-0"><strong>{{ dropshippingFee }}</strong></p>
              </div>
            </div>
            <div class="total-payment mt-3">
              <div class="payment-text">Total</div>
              <div class="payment-text">{{ visibleDropshipper ? totalPayment : totalGoods }}</div>
            </div>
            <div class="next-button">
              <button class="btn btn-next" @click="submitSummary">Continue to Payment</button>
            </div>
          </div>
        </div>

      </div>
    </div>
  </div>
</template>
<script>
import { reactive, ref } from '@vue/reactivity'
import useVuelidate from '@vuelidate/core'
import {required, email } from '@vuelidate/validators'
import cInput from './ui/cInput.vue'
import cTextArea from './ui/cTextArea.vue'
export default {
  components: {
    cInput,
    cTextArea,
  },
  setup() {
    // information form
    const infoForm = reactive({
      email: "",
      phone: "",
      address: "",
      dropshipperName: "",
      dropshipperPhone: "",
    })

    const rulesInfoForm = {
      email: {required, email},
      phone: {required},
      address: {required},
      dropshipperName: {required},
      dropshipperPhone:{required}
    }

    const errorInfoMessage = reactive({
      email: {
        status: "",
        message: "",
      },
      phone: {
        status: "",
        message: ""
      },
      address: {
        status: "",
        message: ""
      },
      dropshipperName: {
        status: "",
        message: ""
      },
      dropshipperPhone: {
        status: "",
        message: ""
      }
    })

    const v$ = useVuelidate(rulesInfoForm, infoForm)

    // dropshipper form
    const visibleDropshipper = ref(false)
    const dropshippingFee = ref(5900)

    // pricing 
    const totalGoods = ref(500000)

    const totalPayment = ref(null)


    // function total
    function handleTotal() {
      if (this.visibleDropshipper) {
        this.totalPayment = parseInt(this.totalGoods) + parseInt(this.dropshippingFee)
      }
    }
    

    const submitSummary = async () => {
      const result = await v$.value.$validate()
      console.log(result)
      if (result) {
        console.log('aaa')
      } else {
        Object.assign(errorInfoMessage, {
          email: {
            status: "is-valid",
            message: "",
          },
          phone: {
            status: "is-valid",
            message: ""
          },
          address: {
            status: "is-valid",
            message: ""
          },
          dropshipperName: {
            status: "is-valid",
            message: ""
          },
          dropshipperPhone: {
            status: "is-valid",
            message: ""
          },
      })
        const errorMessage = v$.value.$errors
        Object.entries(errorMessage).forEach((error) => {
          errorInfoMessage[error[1].$property].status = error[1].$property !== undefined ? 'is-invalid' : 'is-valid'
          errorInfoMessage[error[1].$property].message = error[1].$message
        })
      }
    }

    return {
      infoForm,
      visibleDropshipper,
      errorInfoMessage,
      v$,
      totalGoods,
      totalPayment,
      dropshippingFee,
      handleTotal,
      submitSummary,
    }
  }
}
</script>
<style lang="stylus">
.card-checkout
  padding: 110px 50px 30px
  border-radius 4px
  min-height 550px
.header-step
  display flex
  justify-content space-between
  margin-bottom 36px
  align-items center
.title-step
  font-size 38px
  font-weight 700
  line-height 43px
  color #FF8A00
.border-summary
  border-left 0.5px solid #FF8A00
.summary-info
  text-align left
.title-summary
  font-size 24px
  font-weight 700
  color #FF8A00
.pricing-summary
  text-align left
  margin-top 11rem
.pricing-description
  height: 3rem
.total-payment
  display flex
  justify-content space-between
  align-items center
  color #FF8A00
  font-size 24px
  font-weight 700
.btn-next
  display block !important
  background-color #ff8a00 !important
  width 100%
  color #fff !important
  height 60px
  margin-top 20px
  font-size 18px !important
  font-weight 500 !important
.form-check-input:checked
  background-color #1BD97B !important
  border-color #1BD97B !important
</style>