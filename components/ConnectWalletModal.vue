
<template>
  <div
    v-if="show"
    class="
      modal
      fixed
      w-full
      h-full
      top-0
      left-0
      flex
      items-center
      justify-center
      z-10
    "
  >
    <div
      @click.self="close_modal()"
      class="modal-overlay absolute w-full h-full bg-gray-900 opacity-50"
    ></div>

    <div
      class="
        modal-container
        bg-white
        w-11/12
        md:max-w-md
        mx-auto
        rounded-xl
        shadow-lg
        z-50
        overflow-y-auto
      "
    >
      <div class="modal-content py-4 text-left px-6">
        <div class="flex flex-col">
          <p v-if="!wallet.isConnected" class="text-xl font-bold mb-4">Connect Wallet</p>
          <div v-if="wallet.isConnected">
            <p class="text-xl font-bold mb-2">Your Wallet</p>

            <div v-if="!zilPay" >
              <a class="flex flex-row"><h4 class="text-sm mt-0 font-medium text-gray-600 self-center">Connect wallet</h4></a>
            </div>
            <div v-else-if="wallet.bech32" >
              <a target="_blank" :href="`https://viewblock.io/zilliqa/address/${wallet.bech32}`" class="flex flex-row">  <h4 class="text-sm mt-0 font-medium text-gray-600 self-center hover:underline">{{ wallet.bech32 }}  </h4> <IconLink class="ml-1 h-5 w-5 self-center text-gray-600"/></a>
            </div>
            <div v-else >
              <a class="flex flex-row"><h4 class="text-sm mt-0 font-medium text-gray-600 self-center">Zilpay not found</h4></a>
            </div>
          </div>
        </div>

        <div class="mt-6 bg-gray-100 p-8 rounded-xl ">
          <div class="flex flex-col md:flex-row min-h-12">
            <div class="w-60 flex flex-row mb-6 md:mb-0">
              <svg
                class="h-10 w-10 align-top self-center"
                viewBox="0 0 40 40"
                xmlns="http://www.w3.org/2000/svg"
                xmlns:xlink="http://www.w3.org/1999/xlink"
              >
                <path
                  fill="#52C4C4"
                  d="M18.3939872,39.9294266 C11.8913688,39.2798724 5.99625805,35.8538448 2.81799952,30.8772072 C1.52135566,28.8468612 0.519556056,26.2828619 0.204228194,24.1875173 C0.0628148768,23.2478489 -0.0336421618,21.0583345 0.0110145569,19.8017313 C0.172591526,15.2549668 1.23240762,11.7286888 3.37601174,8.6055399 C4.12655524,7.51202952 4.61680305,6.93858118 5.67221241,5.91966582 C7.35901349,4.29117866 9.05554287,3.14120202 11.4598786,1.99655484 C13.6052171,0.975209677 15.3485606,0.442591 17.6166285,0.115584027 C18.7728061,-0.0511128093 21.412282,-0.0346819259 22.6162303,0.146657372 C26.459262,0.725660601 29.8412021,2.37305407 33.0673034,5.23753969 C36.5109194,8.29514444 38.7940519,11.8661806 39.6272765,15.4979305 C39.9402936,16.862261 39.9963018,17.400483 40,19.0774017 C40.0035213,20.777314 39.9596795,21.2440092 39.6551529,22.7620206 L39.4608509,23.7305807 L38.737802,23.8710072 C36.7618484,24.2547605 34.2312479,24.9417345 32.6353576,25.5276321 C31.4039827,25.9797138 31.1540551,26.0819201 29.3704175,26.8629145 C27.6597326,27.6119667 26.8844926,27.9081188 25.9573677,28.1667338 C24.0196469,28.7072616 21.9508727,28.7530811 20.5533054,28.2864125 C18.672354,27.6583421 17.265524,26.157095 16.9594624,24.4513544 C16.8566891,23.8785339 16.9182324,22.7622915 17.0857265,22.162314 C17.4886981,20.7186017 18.3796084,19.2313341 19.7600287,17.6978614 C20.0153865,17.414183 20.2297742,17.1875437 20.2364447,17.1942184 C20.2429672,17.2005454 20.3256102,17.8174563 20.4197814,18.5643675 C20.5139539,19.3112884 20.5955508,19.929008 20.601125,19.937092 C20.6067117,19.9452207 20.8467103,19.8683502 21.1344976,19.766447 C22.8200479,19.1694248 24.5572794,19.0597253 26.3244517,19.438709 C27.1890108,19.6241225 28.7832251,20.1280238 30.3343546,20.7061503 C30.9329271,20.9292421 31.6045767,21.1492528 31.8269045,21.1950597 C32.8864891,21.4133343 34.6177429,21.1977972 35.7213942,20.7105415 C36.0221693,20.5777088 36.0447396,20.551732 36.1249622,20.2461159 C36.2336225,19.8321664 36.2348418,18.6550162 36.126736,18.1338058 L36.0439938,17.7334237 L34.8214348,16.918159 C27.4573564,12.007387 21.2792105,9.09761778 16.0283654,8.0670495 C14.6004008,7.7867884 12.1124856,7.54635461 12.1124856,7.68861699 C12.1124856,7.72276163 12.0975073,7.78851386 12.0791709,7.83480864 C12.0550615,7.89587235 12.7724276,8.26626542 14.689745,9.18268218 C16.1438653,9.87771616 17.3341177,10.4599619 17.3347406,10.4765559 C17.335439,10.4931698 16.8252554,10.6792861 16.2011585,10.8901724 C14.4230363,11.4910278 13.2311987,11.9658788 12.0187178,12.5565359 C11.0157929,13.0451181 9.56431108,13.8885665 9.56313857,13.9834667 C9.56288717,14.0035174 10.1059411,14.0693723 10.7699202,14.1299463 L11.9771618,14.2400439 L11.3134425,14.9385559 C10.4185972,15.8803179 9.90047389,16.4832872 8.63866422,18.0513333 L7.57013961,19.379188 L8.50422815,19.3958085 C9.0179684,19.4049289 9.4377217,19.4321222 9.43699472,19.4561507 C9.43626845,19.4801778 9.00498234,20.9257825 8.47857015,22.6685813 C7.95216159,24.4113814 7.52676081,25.8426059 7.53323764,25.8490753 C7.53973919,25.8553744 7.98867626,25.7646111 8.53091312,25.6470567 C9.17242239,25.5079571 9.53059787,25.454967 9.5563257,25.495366 C9.57809813,25.5295163 9.69004179,26.9377067 9.80514641,28.6246857 C9.92025103,30.3116661 10.0234249,31.7019693 10.0344168,31.7142559 C10.0454101,31.7265327 10.4362339,31.4209851 10.9029241,31.0352373 C11.3696141,30.6494994 11.7697109,30.3341247 11.7920303,30.3344139 C11.8143498,30.3345535 12.5881982,31.4740673 13.5117121,32.8663468 C14.4352266,34.2586179 15.2109861,35.3991261 15.2356348,35.4008077 C15.2602918,35.4025955 15.6213113,35.0083098 16.0379173,34.5248573 C16.6440529,33.8214779 16.8101405,33.6616851 16.8692033,33.7251321 C16.9097853,33.7687616 17.2198888,34.1439169 17.5582975,34.5588651 C17.8967034,34.9738188 18.4959365,35.6293452 18.8899289,36.0155929 L19.6062709,36.717862 L21.1299151,36.7189793 C23.4973638,36.7207671 24.9984084,36.9660242 26.9922632,37.6776985 L27.5996083,37.8944856 L27.3964918,38.0426957 C26.1980646,38.9172104 24.6786384,39.4961051 22.7468353,39.8141893 C22.1380139,39.9144276 21.6391294,39.9465206 20.4458309,39.9622123 C19.6078254,39.97326 18.6843082,39.9585949 18.393578,39.9294224 L18.3939872,39.9294266 Z"
                  id="path3695"
                ></path>
              </svg>
              <div class="self-center">
                <h4 class="align-middle text-lg font-semibold text-gray-800 ml-2">
                  ZilPay
                </h4>
              </div>
            </div>
            <button
              class="
                flex
                items-center
                justify-center
                w-full
                px-6
                py-2
                text-sm
                font-medium
                text-white
                transition-colors
                duration-200
                transform
                bg-gray-500
                rounded-2xl
                hover:bg-gray-400
                focus:bg-gray-400 focus:outline-none
              "
            >
              <span class="m-2 text-white" @click="handleClick()"
                >
                {{ zilPay ? wallet.bech32 ? 'Connected' : 'Connect wallet' : 'Zilpay not found' }}
                </span
              >
            </button>
          </div>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex'
export default {
  computed: {
    ...mapState({
      wallet: (state) => state.wallet.wallet
    }),
    zilPay() {
      if (process.browser) {
        if (window.zilPay) return window.zilPay;
      }
    },
    network () {
      if (process.browser) {
        return process.env.ZILLIQA_NETWORK
      }
    }
  },
  methods: {
    async handleClick() {
      if (this.wallet.isConnected) {
        this.$router.push({
                    path: '/wallet'
                })
      }

      const isConnect = await window.zilPay.wallet.connect();
      if (isConnect) {
        this.$store.dispatch("wallet/setWallet", {
          bech32: window.zilPay.wallet.defaultAccount.bech32,
          base16: window.zilPay.wallet.defaultAccount.base16,
          isConnected: true,
        });
        localStorage.setItem('wallet', this.zilPay.wallet.defaultAccount.base16)
        this.$store.dispatch('wallet/fetchBalance', this.$store.state.wallet.wallet.bech32)
        this.$nuxt.$emit("walletConnected");
      } else {
        throw new Error("user rejected");
      }
    },
    close_modal() {
      this.$emit("close");
    },
  },
  props: {
    show: Boolean,
  }
};
</script>