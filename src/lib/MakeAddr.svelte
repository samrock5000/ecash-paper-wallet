<script>
  import {
    binToHex,
    hexToBin,
    instantiateSecp256k1,
    instantiateRipemd160,
    instantiateSha256,
    encodeCashAddress,
    CashAddressType,
    encodePrivateKeyWif,
  } from "@bitauth/libauth";
  import QR from "./QR.svelte";
 
  let newWallet;
 
  const log = console.log;
 
  const makeWallet = async (network) => {
    let wallet = {};
    let prefix = network == "mainnet" ? "ecash" : "ectest";
    let byteArray = new Uint8Array(32);
    let randomBytes = window.crypto.getRandomValues(byteArray);
    // let randomBytes = window.crypto.getRandomValues(new Uint8Array(32));
    const secp256k1 = await instantiateSecp256k1();
    const ripemd160 = await instantiateRipemd160();
    const sha256 = await instantiateSha256();
 
    let privKey = encodePrivateKeyWif(sha256, randomBytes, "mainnet");
    const pubKey = secp256k1.derivePublicKeyCompressed(randomBytes);
 
    const pubKeyHash = ripemd160.hash(sha256.hash(pubKey));
    const pubKeyHashHex = binToHex(pubKeyHash);
    let cashType = CashAddressType["P2PKH"];
    const address = encodeCashAddress(
      prefix,
      cashType,
      hexToBin(pubKeyHashHex)
    );
    // let hashData = binToHex(sha256.hash(stringdataBuffer))
    wallet.radomBytes = randomBytes;
    wallet.hexEncoded = binToHex(randomBytes);
    wallet.privateKey = privKey;
    (wallet.address = address), pubKeyHashHex;
    wallet.pubKeyHashHex = pubKeyHashHex;
    wallet.pubKeyHex = binToHex(pubKey);
    return wallet;
  };
 
  let value = "mainnet";
  let network = ["mainnet", "testnet"];
 
  const handleClick = async () => {
    let network = value;
    log("da network! ", network);
    newWallet = makeWallet(network);
  };
</script>
 
<div class="conatainer">
  <div class="select">
    <p>Choose Network</p>
 
    <select bind:value>
      {#each network as item}
        <option value={item}>{item}</option>
      {/each}
    </select>
    <div>
      <button class="btn" on:click|preventDefault={handleClick}
        >NewWallet</button
      >
    </div>
  </div>
 
  {#if newWallet != null}
    {#await newWallet}
      <p>waiting</p>
    {:then items}
      <h5>RandomBytes</h5>
      <p>{items.radomBytes}</p>
      <h5>HexEncoded</h5>
      <p>{items.hexEncoded}</p>
      <h5>To Private Key WIF "wallet import format"</h5>
      <p>{items.privateKey}</p>
      <h5>Public Key</h5>
      <p>{items.pubKeyHex}</p>
      <h5>Public Key Hash</h5>
      <p>{items.pubKeyHashHex}</p>
      <h5>Address</h5>
      <p>{items.address}</p>
      <QR codeValue={items.address} squareSize="200" />
    {/await}
  {/if}
</div>
 
<style>
  @media (max-width: 550px) {
    p {
      font-size: 8px;
    }
  }
 
  @media (min-width: 551px) {
    p {
      font-size: 16px;
    }
  }
 
  .btn {
    margin-top: 1rem;
    border-top: 1px solid #96d1f8;
    background: #65a9d7;
    background: -webkit-gradient(
      linear,
      left top,
      left bottom,
      from(#3e779d),
      to(#65a9d7)
    );
    background: -webkit-linear-gradient(top, #3e779d, #65a9d7);
    background: -moz-linear-gradient(top, #3e779d, #65a9d7);
    background: -ms-linear-gradient(top, #3e779d, #65a9d7);
    background: -o-linear-gradient(top, #3e779d, #65a9d7);
    padding: 5px 10px;
    -webkit-border-radius: 8px;
    -moz-border-radius: 8px;
    border-radius: 8px;
    -webkit-box-shadow: rgba(0, 0, 0, 1) 0 1px 0;
    -moz-box-shadow: rgba(0, 0, 0, 1) 0 1px 0;
    box-shadow: rgba(0, 0, 0, 1) 0 1px 0;
    text-shadow: rgba(0, 0, 0, 0.4) 0 1px 0;
    color: white;
    font-size: 14px;
    font-family: Georgia, serif;
    text-decoration: none;
    vertical-align: middle;
  }
  .btn:hover {
    border-top-color: #28597a;
    background: #28597a;
    color: #ccc;
  }
  .btn:active {
    border-top-color: #1b435e;
    background: #1b435e;
  }
</style>
