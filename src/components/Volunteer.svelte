<script>
  import { namesData as names } from "../data.js";

  import Input from "./Input.svelte";
  import Modal from "./Modal.svelte";

  let volName = "";
  let volPlace = "";
  let volNotes = "";
  let guestVolName = "";
  let checkIn = true;
  let showModal = false;
  let formSubmitted = false;

  //  Get Values of Inputs //

  const setVolName = e => (volName = e.target.value);
  const setVolPlace = e => (volPlace = e.target.value);
  const setVolNotes = e => (volNotes = e.target.value);
  const setGuestVolName = e => (guestVolName = e.target.value);

  // Check that the guest name matches the name pulled from the data file //

  const checkName = (arr, name) =>
    arr.some(el => `${el.firstname} ${el.lastname}` === volName) ? true : false;

  // Check if the checkbox is checked //

  const checkOut = () => (checkIn = !checkIn);

  // Submit the form //

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
      e.preventDefault();
      fetch(scriptURL, {
        method: "POST",
        body: new FormData(form)
      }).then(res => res.json());
      showModal = !showModal;
      setTimeout(function() {
        showModal = !showModal;
      }, 5000);
      document.getElementById("test-form").reset();
      selName.innerHTML = "";
      guestInput.innerHTML = "";
      location.innerHTML = "";
    }
  };
</script>

<style>
  .form {
    background-color: white;
    border-radius: 10px;
    padding-bottom: 10px;
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
    font-size: 26px;
  }

  .form-title {
    font-size: 18px;
    margin: -20px 0;
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
    border-radius: 10px;
  }

  button:hover,
  :focus {
    color: #fff;
    outline: 0;
    box-shadow: 0 0 40px 40px #1e90ec inset, 0 14px 28px rgba(0, 0, 0, 0.25),
      0 10px 10px rgba(0, 0, 0, 0.22);
  }

  .modal-header {
    font-size: 56px;
    margin: 0 auto 1em;
    display: grid;
  }

  .modal-p {
    font-size: 20px;
    margin: 0 auto 1em;
    text-align: center;
  }
</style>

<div class="form">

  <!-- Show the Modal only if the form is submitted -->

  {#if showModal}
    <Modal on:close={() => (showModal = !showModal)}>
      <h2 slot="header" class="modal-header">Thank You!</h2>

      <p class="modal-p">Your form has been submitted.</p>
    </Modal>
  {/if}

  <!-- Form -->

  <form name="submit-to-google-sheet" id="test-form" on:submit={handleSubmit}>

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
      {#if checkIn}
        <h1>Volunteer Check In</h1>
      {:else}
        <h1>Check Out</h1>
      {/if}
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

    <!-- If Guest Visitor is clicked, open new input for name. -->

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

    <!-- If Checkbox is selected, don't show the location box. -->

    {#if checkIn}
      <Input
        label="Location"
        placeholder="What class or location?"
        type="text"
        id="place"
        name="Location"
        required="true"
        className="place"
        bind:value={volPlace}
        onInput={setVolPlace} />

      <Input
        label="Reason for Visiting"
        placeholder="What will you be doing?"
        type="text"
        id="notes"
        name="Notes"
        required="true"
        className="notes"
        bind:value={volNotes}
        onInput={setVolNotes} />
    {/if}

    <button form="test-form" type="submit" id="postForm">Submit</button>

  </form>

</div>
