<template>
  <q-page class="column text-black bg-grey-12" style="padding-bottom: 0px">
    <div class="desktop-version" v-if="screenSize > 1024">
      <div class="row">
        <div class="col col-md-3">
          <div class="wallets-container">
            <profile-header :isMobile="false" class="marg" version="type2222" />
            <wallets :isMobile="false" :showWallets="false" :isWalletsPage="false" :isWalletDetail="false" />
            <!-- <img src="statics/prototype_screens/wallets.jpg" alt=""> -->
          </div>
        </div>
        <div class="col col-md-9">
          <div class="desktop-card-style vtx-converter q-mb-sm">
            <VTXConverter />
          </div>
        </div>
      </div>
    </div>
    <div v-else>
      <profile-header class="marg" version="type3" :fetchCurrentWalletFromState="true" />
      <VTXConverter />
    </div>
  </q-page>
</template>

<script>
import VTXConverter from '../../components/Verto/VTXConverter'
import ProfileHeader from '../../components/Verto/ProfileHeader'
import Wallets from '../../components/Verto/Wallets'

export default {
  components: {
    VTXConverter,
    ProfileHeader,
    Wallets
  },
  data () {
    return {
    }
  },
  created () {
    let exchangeNotif = document.querySelector('.exchange-notif'); if (exchangeNotif !== null) { exchangeNotif.querySelector('.q-btn').dispatchEvent(new Event('click')) }
    this.getWindowWidth()
    window.addEventListener('resize', this.getWindowWidth)
  },
  mounted () {

  },
  methods: {
    getWindowWidth () {
      this.screenSize = document.querySelector('#q-app').offsetWidth
    }
  },
  beforeDestroy () {
    window.removeEventListener('resize', this.getWindowWidth)
  }
}
</script>
<style lang="scss" scoped>
  @import "~@/assets/styles/variables.scss";

  /deep/ .profile-wrapper--header{
    margin-bottom: 0px;
  }
  /deep/ .wallets-wrapper{
    padding-bottom: 0px !important;
  }
  /deep/ .wallets-wrapper--list{
    box-shadow: none;
    margin-top: 0px;
  }
  .marg{
    /deep/ .profile-wrapper{
      &--header{
        margin-bottom: 0px;
      }
    }
  }
  .mobile-pad{
    padding-bottom: 50px
  }
  .desktop-version{
    background: #E7E8E8;
    padding-top: 13vh;
    padding-left: 12vh;
    padding-bottom: 50px;
    padding-right: 2%;
  }
  .desktop-card-style{
    height: 100%;
  }
  .vtx-converter{
    /deep/ .vtx-converter-wrapper{
      padding: 0px;
      .list-wrapper--chain__eos-to-vtx-convertor{
        box-shadow: none;
        padding: 0%;
      }
    }
  }
</style>
