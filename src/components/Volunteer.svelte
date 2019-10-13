<script>
  import { onMount } from "svelte";

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

  const handleSubmit = () => {
    const selName = document.getElementById("volunteersList");
    const guestInput = document.getElementById("guest");
    const location = document.getElementById("place");

    if (selName.selectedIndex < 1) {
      alert("Please select your name.");
      selName.focus();
    } else if (location.value.length < 1) {
      alert("Please input your location.");
      location.focus();
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

      showModal = !showModal;
      setTimeout(function() {
        showModal = !showModal;
      }, 5000);
      document.getElementById("test-form").reset();
    });
  });
</script>

<style>
  .form {
    align-self: center;
    background-color: white;
    margin: 0 auto;
    width: 50vw;
    padding: 0 0.5em;
    max-height: 100%;
    border-radius: 10px;
  }
  #test-form {
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

  .form-title {
    font-size: 18px;
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .checkContainer {
    display: flex;
    margin: 0 auto 18px;
    align-items: center;
    justify-content: flex-start;
    color: red;
  }

  input[type="checkbox"] {
    visibility: hidden;
  }

  #checklabel {
    height: 35px;
    width: 35px;
    background-color: rgb(255, 255, 255);
    border: 3px inset #1e90ec;
    margin-right: 10px;
    display: block;
  }

  input[type="checkbox"]:checked + label {
    border: 2px solid black;
    font-size: 24px;
  }
</style>

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

<div class="form">

  {#if showModal}
    <Modal on:close={() => (showModal = !showModal)}>
      <h2 slot="header" class="modal-header">Thank You!</h2>
      <p>Your form has been submitted.</p>
    </Modal>
  {/if}

  <form name="submit-to-google-sheet" id="test-form">
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

    <p style="color: red;">
      **If the visitor is not in the system, use the Guest Visitor name and a
      new input box will come up for the guests name.
    </p>
  </form>

</div>
