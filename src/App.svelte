<script>
  import Volunteer from "./components/Volunteer.svelte";
</script>

<style>
  .body {
    display: grid;
    overflow: none;
    height: 100vh;
    grid-template-rows: 150px 1fr;
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
    height: 100%;
    background-color: #111;
    display: grid;
    text-align: center;
    align-content: center;
  }

  p {
    margin-top: -5%;
    color: white;
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
    <p>
      If you are not volunteering, please use the book to sign in.
      <br />
      (ie. visiting for lunch, dropping off something, picking up)
    </p>
    <Volunteer />
  </main>
</div>
