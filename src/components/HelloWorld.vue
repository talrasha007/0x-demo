<template>
  <div class="hello">
    account: {{account}}<br/>
    {{addresses}}
  </div>
</template>

<script>
import { Web3Wrapper } from '@0x/web3-wrapper';
import { getContractAddressesForNetworkOrThrow } from '@0x/contract-addresses';

export default {
  name: 'HelloWorld',

  async mounted() {
    const accounts = await window.ethereum.enable();
    this.$data.account = accounts[0];

    const web3Wrapper = new Web3Wrapper(window.ethereum);
    const networkId = await web3Wrapper.getNetworkIdAsync();
    this.$data.addresses = getContractAddressesForNetworkOrThrow(networkId);
  },

  data() {
    return {
      account: '',
      addresses: {}
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
