<script>
  import Volunteer from "./components/Volunteer.svelte";
  import Info from "./components/Info.svelte";
</script>

<style>
  .body {
    display: grid;
    grid-template-rows: 150px 1fr 150px;
    height: 98vh;
    font-family: "Montserrat", sans-serif;
  }

  header {
    height: 150px;
    color: #111;
    display: grid;
    grid-template-columns: 1fr 150px;
    align-items: center;
    padding: 0 1em;
  }
  h1 {
    font-size: 40px;
  }
  .logo {
    justify-self: flex-end;
    width: 150px;
    height: 150px;
  }

  main {
    background-color: #111;
    display: grid;
    align-content: center;
    align-items: center;
  }

  .vol {
    margin: 1em auto;
    padding: 1em 0;
    display: grid;
    justify-content: center;
  }

  @media (max-width: 550px) {
    h1 {
      font-size: 24px;
    }
  }
</style>

<div class="body">
  <header class="header">
    <div class="school">
      <h1>
        Waukazoo Elementary
        <br />
        <span>Visitor Check In</span>
      </h1>
    </div>

    <img src="./logo.png" alt="logo" class="logo" />
  </header>
  <main>

    <div class="vol">
      <Volunteer />
    </div>

  </main>

  <Info />

</div>
