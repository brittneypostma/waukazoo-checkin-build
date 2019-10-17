<script>
  import Volunteer from "./components/Volunteer.svelte";
  import Info from "./components/Info.svelte";
</script>

<style>
  .body {
    display: grid;
    grid-template-rows: 138px 5fr 1fr;
    width: 100vw;
    height: 98vh;
    font-family: "Montserrat", sans-serif;
  }

  header {
    position: relative;
    top: -5%;
    height: 150px;
    color: #111;
    display: grid;
    grid-template-columns: 1fr 150px;
    align-content: center;
    padding: 0 1em;
    background-color: white;
  }

  .school {
    display: flex;
    align-items: center;
  }

  .wo {
    width: 175px;
    height: 90px;
    margin-right: 1em;
    position: relative;
    top: 1%;
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
    padding: 1em 0;
    display: grid;
    justify-content: center;
  }

  @media (max-width: 676px) {
    .header {
      grid-template-columns: 150px 1fr;
    }
    .wo {
      display: none;
    }
    h1 {
      font-size: 28px;
      grid-row: 1/2;
      grid-column: 2/3;
    }
    .logo {
      grid-row: 1/2;
      justify-self: flex-start;
    }
  }
</style>

<div class="body">
  <header class="header">
    <div class="school">

      <img src="./wo.png" alt="wo" class="wo" />
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
