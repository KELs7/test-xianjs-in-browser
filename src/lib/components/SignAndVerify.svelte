<script>
  import { Wallet } from "../../../xian-js/index.mjs";
  import { Buffer } from "buffer";

  let msg1 = "";
  let msg2 = "";
  //let sk = "69a8db3fb7196debc2711fad1fa1935918d09f5d8900d84c3288ea5237611c03"
  let sm1 = "";
  let sm2 = "";
  let string = "";
  let messageBytes = "";
  let verified = "";
  let vk = "";
  let sk = "";

  const gmb = ()=>{
    const stringBuffer = Buffer.from(msg1.trim());
    return new Uint8Array(stringBuffer);
  }

  const getMessageBytes = ()=>{

    messageBytes = gmb();
    console.log(messageBytes);
  }

  const signMessage = ()=>{
    // const stringBuffer = Buffer.from(message.trim());
    // const messageBytes = new Uint8Array(stringBuffer); 
    const msgb = gmb();  
    sm1 = Wallet.sign(sk.trim(), msgb)
 }
  const verifySignature = ()=>{
    const stringBuffer = Buffer.from(msg2.trim());
    const messageBytes = new Uint8Array(stringBuffer);
    verified = Wallet.verify(vk, messageBytes, sm2)
  }
</script>

<div style="margin-top: 1.25rem;">
  <label for="Sign And Verify"><h2>Sign And Verify</h2></label> 
  <div style="margin-top: 1rem;">
    <input placeholder="message" class="box" bind:value={msg1} type="text">
  </div>    
  <div style="margin-top: 0.7rem;">
    <input placeholder="sk" class="box" bind:value={sk} type="text">
  </div>
  <div class="box" style="margin-top: 1rem; overflow: auto;">
    Signed: 
    {sm1}
  </div> 
  <button class="butt" style="margin-top: 1rem;"  on:click={signMessage}>Sign Message</button>
    <!-- verify -->
  <div style="margin-top: 1rem;">
    <div >
      <input placeholder="vk" class="box" bind:value={vk} type="text">
    </div>
    <div style="margin-top: 1rem;">
      <input placeholder="message" class="box" bind:value={msg2} type="text">
    </div>    
    <div style="margin-top: 0.7rem;">
      <input placeholder="signed message" class="box" bind:value={sm2} type="text">
    </div>
    <div class="box" style="margin-top: 1rem; overflow: auto;">
      verified: 
      {verified}
    </div> 
    <button class="butt" style="margin-top: 1rem;"  on:click={verifySignature}>Verify Signature</button>
  </div>
</div>

<style>
  .butt {
    font-size: 1rem;
    padding: 0.5rem;
    margin-top: 1rem;
  }

  .box {
    border: 2px solid black; 
    padding: 0.6rem; 
    width: 36rem;
  }
</style>
