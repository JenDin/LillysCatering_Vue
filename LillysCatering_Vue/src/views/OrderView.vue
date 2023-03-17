<!-- HTML code -->
<template>
  <h1 class="text-4xl text-center uppercase font-bold mt-8 mb-6">Order catering</h1>

  <section class="container xl:flex max-w-[1100px] mb-36 w-[95%] mx-auto">
    <!-- Image on larger screens -->
    <div class="hidden xl:w-1/2 p-4 xl:flex justify-center items-center bg-[#e5d9f2]">
      <div>
        <p class="p-1 lg:w-5/6 mx-auto mb-12 text-5xl font-bold">
          Let’s make your next event unforgettable.
        </p>
      </div>
    </div>

    <div
      class="hidden xl:block max-w-[90%] m-auto md:m-0 lg:max-w-full border-2 h-auto relative top-0 border-black"
    ></div>

    <div class="xl:w-1/2 flex items-center justify-center p-8">
      <div class="mx-auto w-full sm:w-10/12 lg:w-[500px] lg:max-w-[500px]">
        <!-- Confirmation message above the form -->
        <div class="mb-6" v-if="successMsg">
          <p class="text-center font-semibold text-green-700">
            Thank you for ordering from Lilly's Catering!
          </p>
        </div>

        <!-- Booking form -->
        <form class="p-6 w-[90%] mx-auto max-w-lg" @submit.prevent="addBooking()">
          <!-- Full name -->
          <div class="mb-3">
            <label for="name" class="mb-0 block text-base font-normal"> Full name </label>
            <input
              type="text"
              name="fullName"
              v-model="fullName"
              class="w-full border border-black bg-white py-1 px-2 text-base"
            />
            <!-- Full name error message -->
            <span v-if="fullNameErrorMsg" class="text-sm text-customRed mt-0.5">
              * Please enter your full name
            </span>
          </div>

          <!-- PhoneNo -->
          <div class="mb-3">
            <label for="phoneNo" class="mb-0 block text-base font-normal"> Phone number </label>
            <input
              type="text"
              name="phoneNo"
              v-model="phoneNo"
              class="w-full border border-black bg-white py-1 px-2 text-base"
            />
            <!-- PhoneNo error message -->
            <span v-if="phoneNoErrorMsg" class="text-sm text-customRed mt-0.5">
              * Please enter a phone number
            </span>
          </div>

          <!-- Order & guest amount -->
          <div class="mb-2">
            <label for="subject" class="mb-0 block text-base font-normal">
              Order & guest amount
            </label>
            <textarea
              id="order"
              name="order"
              class="border border-black px-2 pt-2"
              v-model="order"
            ></textarea>
            <!-- Order & guest amount error message -->
            <p v-if="orderErrorMsg" class="text-sm text-customRed mt-0.5">
              * Please enter an order and guest amount
            </p>
          </div>

          <!-- Address -->
          <div class="mb-3">
            <label for="address" class="mb-0 block text-base font-normal"> Address </label>
            <input
              type="text"
              name="address"
              v-model="address"
              class="w-full border border-black bg-white py-1 px-2 text-base"
            />
            <!-- Address error message -->
            <p v-if="addressErrorMsg" class="text-sm text-customRed mt-0.5">
              * Please enter an address
            </p>
          </div>

          <!-- Date -->
          <div class="mb-3">
            <label for="email" class="mb-0 block text-base font-normal"> Date </label>

            <Datepicker
              class="border border-black bg-white mb-4"
              v-model="date"
              :min-date="minDate"
              :enable-time-picker="false"
            />

            <!-- Date error message -->
            <p v-if="dateErrorMsg" class="text-sm text-customRed mt-0.5">* Please enter a date</p>
          </div>

          <Button btnText="Book" />
        </form>
      </div>
    </div>
  </section>
  <Footer />
</template>

<!-- JavaScript code -->
<script>
import Button from '../components/Button.vue'
import Footer from '../components/Footer.vue'

const date = new Date()

export default {
  components: {
    Button,
    Footer
  },
  data() {
    return {
      fullName: '',
      phoneNo: '',
      order: '',
      address: '',
      date: '',
      fullNameErrorMsg: false,
      phoneNoErrorMsg: false,
      orderErrorMsg: false,
      addressErrorMsg: false,
      dateErrorMsg: false,
      isSent: false,
      successMsg: false,
      minDate: `${date.getFullYear()}-${date.getMonth() + 2}`
    }
  },
  computed: {
    fullNameErrorMsg() {
      if (this.fullName === '' && this.isSent) {
        return true
      }
      return false
    },
    phoneNoErrorMsg() {
      if (this.phoneNo === '' && this.isSent) {
        return true
      }
      return false
    },
    orderErrorMsg() {
      if (this.order === '' && this.isSent) {
        return true
      }
      return false
    },
    addressErrorMsg() {
      if (this.address === '' && this.isSent) {
        return true
      }
      return false
    },
    dateErrorMsg() {
      if (this.date === '' && this.isSent) {
        return true
      }
      return false
    }
  },
  methods: {
    async addBooking() {
      this.isSent = true

      const bookingBody = {
        name: this.fullName,
        phoneNo: this.phoneNo,
        order: this.order,
        address: this.address,
        date: this.date
      }

      if (
        this.fullName !== '' &&
        this.phoneNo !== '' &&
        this.order !== '' &&
        this.address !== '' &&
        this.date !== ''
      ) {
        const resp = await fetch('https://localhost:7235/api/bookingapi', {
          method: 'POST',
          headers: {
            Accept: 'application/json',
            'Content-type': 'application/json'
          },
          body: JSON.stringify(bookingBody)
        })

        const data = await resp.json()

        this.fullName = ''
        this.phoneNo = ''
        this.order = ''
        this.address = ''
        this.date = ''
        this.isSent = false
        this.successMsg = true
      }
    }
  }
}
</script>

<!-- CSS styles -->
<style scoped>
textarea {
  width: 100%;
  height: 70px;
  resize: none;
}
</style>
