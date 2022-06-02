<script>
    import { onMount } from 'svelte';
      
      export let codeValue;
      export let squareSize; 
      
    let qrcode;
              
      onMount(() => {
  
          let script = document.createElement('script');
      script.src = "https://cdn.rawgit.com/davidshimjs/qrcodejs/gh-pages/qrcode.min.js"
      document.head.append(script);
      
          script.onload = function() {
  
              qrcode = new QRCode("qrcode", {
                  text: codeValue,
                width: squareSize,
          height: squareSize,
          colorDark : "#000000",
          colorLight : "#C9CAD6",
          correctLevel : QRCode.CorrectLevel.H
              });		
              
          };				
        
      });
  </script>
  
  <style>
    #qrcode { 
      width:20px;
      height:200x;
      margin-top:15px;
    }

    .container{
        display: flex;
        justify-content: center;
        margin-right: 11rem;
    }
  </style>
  <div class="container">
    <div id="qrcode"></div>
  
  </div>
  
  