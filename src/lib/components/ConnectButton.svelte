<script lang="ts">
  import { connected, chainId, signerAddress, defaultEvmStores } from 'svelte-ethers-store'
  import Web3Modal from 'web3modal'
  import detectEthereumProvider from '@metamask/detect-provider'
  import {truncateAddress} from '$lib/utils';

  const connect = async () => {
    const web3Modal = new Web3Modal({
      providerOptions: {
        injected: {
          package: detectEthereumProvider(),
        },
      },
    })
    const provider = await web3Modal.connect()
    defaultEvmStores.setProvider(provider)
  }

</script>

{#if !$connected}

<button type="button" on:click={(e) => connect()}>Connect</button>

{:else}

<!-- <p>Connected to chain (id {$chainId}) with account ({$signerAddress})</p> -->
{truncateAddress($signerAddress)}

{/if}