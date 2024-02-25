<script>
  import { Wallet } from "../../../xian-js/index.mjs"

  let keyPair = {vk: "", sk: ""};
  let seed;
  let derivationIndex;
  let bip39 = {derivationIndex: "", mnemonic: "", seed: "", vk: "", sk: ""}; 
  let vk = "";
  let sk;
  
  const createKeyPair = ()=>{
    keyPair = Wallet.new_wallet();
  }

  const createBIP39Wallet = ()=>{
    const i = derivationIndex || 0
    if(!seed) seed = undefined;
    const s = seed === undefined? seed : seed.trim();
    bip39 = Wallet.new_wallet_bip39(s, i );
  }
  
  const getVkFromSK = ()=>{
    vk = Wallet.get_vk(sk);
  }
  
</script>

<div>
  <label for="Create Wallet"><h2>Create Wallet</h2></label>  
  <div style="margin-top: 1rem;">
    <div class="box">
      <p>vk: {keyPair.vk} </p>
      <p>sk: {keyPair.sk}<p>
    </div>
    <button class="butt" on:click={createKeyPair}>Create Keypair</button>
  </div>
  <div style="margin-top: 1.25rem;">
    <div class="box" style="height: 10.2rem; overflow: auto;">
      <p>derivationIndex: {bip39.derivationIndex}</p>
      <p>mnemonic: {bip39.mnemonic}</p>
      <p>seed: {bip39.seed}</p>
      <p>vk: {bip39.vk}</p>
      <p>sk: {bip39.sk}<p> 
    </div>
    <div>
        <input placeholder="seed: optional (128 characters in hex)" class="box" bind:value={seed} type="text">
        <input placeholder="derivationIndex: optional (default = 0)" class="box" bind:value={derivationIndex} type="number">
    </div>
    <button class="butt" on:click={createBIP39Wallet}>Create BIP39 Wallet</button>
  </div>
  <div style="margin-top: 1rem;">
    <div>
      <input placeholder="sk" class="box" bind:value={sk} type="text">
    </div>
    <div class="box" style="margin-top: 1rem; overflow: auto;">
      vk: 
      {vk}
    </div>
    <button class="butt" on:click={getVkFromSK}>Get vk</button>
  </div>
</div>

<style>
  .butt {
      font-size: 1rem;
      padding: 0.5rem;
      margin-top: 1rem;
  }
  p {
    font-size: 1.1rem;
  }
  .box {
    border: 2px solid black; 
    padding: 0.6rem; 
    width: 36rem;
  }
</style>
