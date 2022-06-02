<script>
import MakeAddr from "./lib/MakeAddr.svelte";
</script>

<main>
  
  <div class="container">
    <h1>eCash</h1>
    <h2>Paper wallet</h2>
    <MakeAddr/>
  </div>
</main>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
      background: rgb(201,202,214);
      background: radial-gradient(circle, rgba(201,202,214,0.4514180672268907) 9%, rgba(30,43,212,0.14609593837535018) 75%);

  }
 
  main {
    text-align: center; 
    padding: 1em;
    margin: 0 auto;
  }

  h1 {
    color: #354479;
    font-size: 2rem;
    font-weight: 700;
    line-height: 1.1;
    margin: 4rem auto 0.2rem;
    max-width: 14rem;
  }

  h2 {
    color: #354479;
    font-size: 2rem;
    font-weight: 700;
    line-height: 1.1;
    margin: 0.1rem auto 1rem;
    max-width: 14rem;
  }


  
  .container{
        display: flex;
        justify-content: center;
        flex-direction: column;
    }
  
</style>
