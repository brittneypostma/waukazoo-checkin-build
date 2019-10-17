<script>
  import { namesData as data } from "../data.js";
  export let required = false;
  export let placeholder = "";
  export let type = "text";
  export let name = "";
  export let value = "";
  export let onInput = "";
  export let id;
  export let label;
  export let className;

  // makes value reactive
  $: if (!value) value = "";

  let clickedSearch = false;
  const handleToggleSearch = () => {
    clickedSearch = !clickedSearch;
  };

  function handleInputName() {
    let input = document.getElementById("volunteersList");
    let li = document.querySelectorAll("ul li");
    li.forEach(item => {
      item.onclick = function(e) {
        let txt = this.innerText;
        let inputTxt = input.innerHTML;
        value = txt;
        handleToggleSearch();
      };
    });
  }

  function filterFunction() {
    let input = document.getElementById("volunteersList");
    let filter = input.value.toUpperCase();
    let li = document.getElementsByTagName("li");
    for (let i = 0; i < li.length; i++) {
      let txtValue = li[i].textContent || li[i].innerText;
      if (txtValue.toUpperCase().indexOf(filter) > -1) {
        li[i].style.display = "";
      } else {
        li[i].style.display = "none";
      }
    }
  }
</script>

<style>
  input {
    outline: none;
    width: 100%;
    padding: 12px 20px;
    border: 1px solid #ddd;
    margin-bottom: 0;
    border-radius: 10px;
  }

  input:focus {
    border: 1px solid #1e90ec;
  }

  input:focus:first-child {
    border-radius: 10px 10px 0 0;
  }

  .displayList {
    width: 100%;
  }

  #myUL {
    width: 105%;
    margin: 0;
    max-height: 165px;
    overflow-y: scroll;
    overflow-x: hidden;
    list-style-type: none;
    padding: 0;
    animation-duration: 0.3s;
    animation-delay: 0.3s;
    border-radius: 0 0 10px 10px;
  }

  li {
    border: 1px solid #ddd;
    margin-top: -1px; /* Prevent double borders */
    background-color: #ffffff;
    padding: 2px;
    text-decoration: none;
    font-size: 16px;
    color: black;
    display: block;
    opacity: 1;
    transform: translate(0, -200px);
    animation-direction: normal;
    animation-iteration-count: 1;
    animation-timing-function: ease-in-out;
    animation-fill-mode: forwards;
    animation-name: dropin;
    animation-duration: 0.6s;
  }

  @keyframes dropin {
    0% {
      opacity: 0;
      transform: translate(0, -200px);
    }
    100% {
      opacity: 1;
      transform: translate(0, 0);
    }
  }
  @-webkit-keyframes dropin {
    0% {
      opacity: 0;
      transform: translate(0, -200px);
    }
    0% {
      opacity: 0.5;
      transform: translate(0, -100px);
    }
    100% {
      opacity: 1;
      transform: translate(0, 0);
    }
  }

  li:nth-child(odd) {
    background-color: #ddd;
  }

  li:nth-child(even) {
    background-color: #eee;
  }

  li {
    background-color: rgb(255, 255, 255);
    transition: all 0.2s ease;
  }

  li:hover {
    background-color: #333;
    color: white;
    cursor: pointer;
  }

  label {
    font-weight: 700;
    font-size: 1.2rem;
    display: flex;
  }
</style>

<label for={id}>{label}</label>
{#if id === 'volunteersList'}
  <div class="displayList">
    <input
      {required}
      {name}
      {className}
      {placeholder}
      {id}
      autocomplete="off"
      bind:value
      on:click={handleToggleSearch}
      on:input={onInput}
      on:keyup={filterFunction} />
    {#if clickedSearch}
      <ul id="myUL">
        {#each data as name}
          <li on:mouseenter={handleInputName}>
            {name.firstname} {name.lastname}
          </li>
        {/each}
      </ul>
    {/if}
  </div>
{:else if type === 'text'}
  <input
    {required}
    {name}
    {id}
    {placeholder}
    {className}
    bind:value
    autocomplete="off"
    on:input={onInput} />
{/if}
