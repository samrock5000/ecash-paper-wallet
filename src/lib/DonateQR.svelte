<script>
import { onMount } from 'svelte';

export const addr = 'ecash:qqwp0j423n9wenhd9dkmgr06cm7g2m7mmvgsa3hnmc'

export let codeValue;
      export let squareSize; 
      
    let qrcode;
              
      onMount(() => {
  
          let script = document.createElement('script');
      script.src = "https://cdn.rawgit.com/davidshimjs/qrcodejs/gh-pages/qrcode.min.js"
      document.head.append(script);
      
          script.onload = function() {
  
              qrcode = new QRCode("qrcode2", {
                  text: codeValue,
                width: squareSize,
                height: squareSize,
                colorDark : "#000000",
                colorLight : "#C9CAD6",
         
              });		
              
          };				
        
      });


</script>


    <div class="container">
        <div id="qrcode2"></div>
      </div>
 
      <style>
        #qrcode2 { 
          width:20px;
          height:200x;
          margin-top:1rem;
        }
    
        .container{
            display: flex;
            justify-content: center;
            margin-right: 11rem;
        }
      </style>
      