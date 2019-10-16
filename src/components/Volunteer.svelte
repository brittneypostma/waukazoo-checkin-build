<script>
  import { onMount } from "svelte";
  import { namesData as names } from "../data.js";

  import Input from "./Input.svelte";
  import Modal from "./Modal.svelte";

  let volName = "";
  let volPlace = "";
  let guestVolName = "";
  let checkIn = true;
  let showModal = false;

  const setVolName = e => (volName = e.target.value);
  const setVolPlace = e => (volPlace = e.target.value);
  const setGuestVolName = e => (guestVolName = e.target.value);

  const checkName = (arr, name) =>
    arr.some(el => `${el.firstname} ${el.lastname}` === volName) ? true : false;

  // const post = () => {
  //   const scriptURL =
  //     "https://script.google.com/macros/s/AKfycbzrKqVJEidj98LDaebjqwQX4Ti5tjvWcx52oLBrQwKqDH29_uo/exec";
  //   const form = document.forms["submit-to-google-sheet"];

  //   form.addEventListener("submit", e => {
  //     e.preventDefault();
  //     fetch(scriptURL, {
  //       method: "POST",
  //       body: new FormData(form)
  //     });
  //     showModal = !showModal;
  //     setTimeout(function() {
  //       showModal = !showModal;
  //     }, 5000);
  //   });
  // };

  const handleSubmit = e => {
    const selName = document.getElementById("volunteersList");
    const guestInput = document.getElementById("guest");
    const location = document.getElementById("place");
    const selVal = selName.value;

    const scriptURL =
      "https://script.google.com/macros/s/AKfycbzrKqVJEidj98LDaebjqwQX4Ti5tjvWcx52oLBrQwKqDH29_uo/exec";
    const form = document.forms["submit-to-google-sheet"];

    const check = checkName(names, selVal);

    if (location === "") {
      alert("Please input your location.");
      location.focus();
      return false;
    } else if (guestInput === "") {
      alert("Please input your name in the Guest Visitor box.");
      guestInput.focus();
      return false;
    } else if (!check) {
      alert("Please select your name or Guest Visitor from the list.");
      e.preventDefault();
      selName.focus();
      return false;
    } else {
      form.addEventListener("submit", e => {
        e.preventDefault();
        fetch(scriptURL, {
          method: "POST",
          body: new FormData(form)
        });
        showModal = !showModal;
        setTimeout(function() {
          showModal = !showModal;
        }, 5000);
        document.getElementById("test-form").reset();
      });
    }
  };

  const checkOut = () => {
    checkIn = !checkIn;
  };
</script>

<style>
  .form {
    background-color: white;
    padding: 1em;
    border-radius: 10px;
  }

  .checkContainer {
    display: flex;
    margin: 0 auto;
    align-items: center;
    color: red;
    font-weight: 600;
  }

  input[type="checkbox"] {
    visibility: hidden;
  }

  #checklabel {
    height: 30px;
    width: 30px;
    background-color: rgb(255, 255, 255);
    border: 3px inset #1e90ec;
    margin-right: 10px;
    display: grid;
    justify-content: center;
  }

  input[type="checkbox"]:checked + label {
    font-size: 24px;
  }

  .form-title {
    font-size: 18px;
    margin: -20px 0 0;
    padding: 0;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  #test-form {
    margin: 1em 2em;
    display: grid;
    align-items: center;
    justify-content: center;
    grid-gap: 10px;
  }

  button {
    width: 100%;
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
</style>

<div class="form">

  {#if showModal}
    <Modal on:close={() => (showModal = !showModal)}>
      <h2 slot="header" class="modal-header">Thank You!</h2>
      <p>Your form has been submitted.</p>
    </Modal>
  {/if}

  <form name="submit-to-google-sheet" id="test-form">

    <div class="checkContainer">
      <input
        type="checkbox"
        value="None"
        id="mycheck"
        name="check"
        on:click={checkOut} />
      <label id="checklabel" for="mycheck">
        {#if !checkIn}&#10003;{/if}
      </label>
      <p>Check box to check out.</p>
    </div>

    <div class="form-title">
      <h1>Volunteer Check In</h1>
    </div>

    <Input
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
        placeholder="Where will you be volunteering?"
        type="text"
        id="place"
        name="Location"
        required="true"
        className="place"
        bind:value={volPlace}
        onInput={setVolPlace} />
    {/if}

    <button
      form="test-form"
      type="submit"
      id="postForm"
      on:click={handleSubmit}>
      Submit
    </button>

  </form>

</div>
