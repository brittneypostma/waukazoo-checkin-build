<script>
  import { onMount } from "svelte";

  import Input from "./Input.svelte";

  const date = new Date();
  const dd = date.getDate();
  const mm = date.getMonth() + 1;
  const yy = date.getFullYear();
  const today = `${mm}/${dd}/${yy}`;
  const time = date.toLocaleTimeString([], {
    hour: "2-digit",
    minute: "2-digit"
  });

  let volName = "";
  let volPlace = "";
  let guestVolName = "";
  let checkIn = true;

  const setVolName = e => (volName = e.target.value);
  const setVolPlace = e => (volPlace = e.target.value);
  const setGuestVolName = e => (guestVolName = e.target.value);

  const handleSubmit = () => {
    const selName = document.getElementById("volunteersList");
    const guestInput = document.getElementById("guest");
    const location = document.getElementById("class");

    if (selName.selectedIndex < 1) {
      alert("Please select your name.");
      selName.focus();
      return false;
    } else if (guestInput.innerText === "") {
      alert("Please select your name.");
      guestName.focus();
      return false;
    } else if (location.value.length < 1) {
      alert("Please input your location.");
      location.focus();
      return false;
    }
  };

  const checkOut = () => {
    checkIn = !checkIn;
  };

  onMount(() => {
    const scriptURL =
      "https://script.google.com/macros/s/AKfycbzrKqVJEidj98LDaebjqwQX4Ti5tjvWcx52oLBrQwKqDH29_uo/exec";
    const form = document.forms["submit-to-google-sheet"];

    form.addEventListener("submit", e => {
      e.preventDefault();
      fetch(scriptURL, {
        method: "POST",
        body: new FormData(form)
      });
      document.getElementById("test-form").reset();
    });
  });
</script>

<style>
  /* .form {
    align-self: center;
    background-color: white;
    margin: 0 auto;
    width: 50vw;
    padding: 0 0.5em;
    max-height: 60vh;
    border-radius: 10px;
  } */
  #test-form {
    background-color: white;
    margin: 1em 2em;
    display: grid;
    align-items: center;
    justify-content: center;
    grid-gap: 10px;
  }

  #postForm {
    width: 100%;
  }

  button {
    background-color: transparent;
    border: 2px solid #1e90ec;
    color: #1e90ec;
    cursor: pointer;
    font-size: 16px;
    line-height: 1;
    padding: 16px;
    text-decoration: none;
    text-align: center;
    text-transform: uppercase;
    font-weight: 700;
    transition: box-shadow 300ms ease-in-out, color 300ms ease-in-out;
    margin-bottom: -10px;
  }

  button:hover,
  :focus {
    color: #fff;
    outline: 0;
    box-shadow: 0 0 40px 40px #1e90ec inset, 0 14px 28px rgba(0, 0, 0, 0.25),
      0 10px 10px rgba(0, 0, 0, 0.22);
  }

  .date {
    margin: 0 0 -20px;
    padding: 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .checkContainer {
    display: flex;
    width: 50%;
    justify-content: flex-start;
    color: red;
  }

  input[type="checkbox"] {
    visibility: hidden;
  }

  #checklabel {
    height: 50px;
    width: 50px;
    background-color: #f44;
    display: block;
    border-radius: 100%;
  }

  input[type="checkbox"]:checked + label {
    border: 2px solid black;
  }

  /* .checkContainer label {
    font-size: 18px;
  } */

  /* input[type="checkbox"] {
    width: 20px;
    height: 20px;
    border-radius: 10px;
    border: 2px solid #1e90ec;
    color: #1e90ec;
    cursor: pointer;
    line-height: 1;
    padding: 16px;
    text-decoration: none;
    text-align: center;
    text-transform: uppercase;
    font-weight: 700;
    transition: box-shadow 300ms ease-in-out, color 300ms ease-in-out;
    margin-right: 10px;
  }

  input[type="checkbox"]:checked {
    background: blue;
    color: white;
  } */
</style>

<div class="form">

  <form name="submit-to-google-sheet" id="test-form">
    <div class="date">
      <h2>{today}</h2>
      <h2>Volunteer Check In</h2>
      <h2>{time}</h2>
    </div>

    <Input
      class="volInput"
      label="Volunteer Name"
      id="volunteersList"
      type="text"
      name="Name"
      placeholder="&#x1F50D; Search Names..."
      required="true"
      bind:value={volName}
      className="volName"
      onInput={setVolName} />

    {#if volName === 'Guest Visitor'}
      <Input
        label="Guest Name"
        id="guest"
        type="text"
        required="true"
        placeholder="Guest Name"
        bind:value={guestVolName}
        className="guestName"
        name="Other"
        onInput={setGuestVolName} />
    {/if}

    {#if checkIn}
      <Input
        label="Location"
        type="text"
        id="place"
        name="Location"
        required="true"
        className="place"
        bind:value={volPlace}
        onInput={setVolPlace} />
    {/if}
    <br />
    <div class="checkContainer">

      <input
        type="checkbox"
        value="None"
        id="mycheck"
        name="check"
        on:click={checkOut} />
      <label id="checklabel" for="mycheck">&#10003;</label>

    </div>
    <button
      form="test-form"
      type="submit"
      id="postForm"
      on:click={handleSubmit}>
      Submit
    </button>

    <p style="color: red;">
      **If the visitor is not in the system, use the Guest Visitor name and a
      new input box will come up for the guests name.
    </p>
  </form>

</div>
