<script>
  import Volunteer from "./components/Volunteer.svelte";
  import Info from "./components/Info.svelte";
</script>

<style>
  .body {
    display: grid;
    grid-template-rows: 138px 5fr 1fr;
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
    align-items: flex-start;
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

  @media (max-width: 550px) {
    h1 {
      font-size: 24px;
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
