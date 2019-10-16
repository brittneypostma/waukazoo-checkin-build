<style>
  .info {
    font-size: 14px;
    display: grid;
    justify-items: center;
  }

  .spans {
    display: grid;
    margin: 0;
  }

  .list {
    background-image: linear-gradient(#111, white);
  }

  .ol-list {
    display: flex;
    list-style-type: none;
    margin: 10px;
    justify-items: center;
  }

  .steps {
    display: grid;
    font-size: 14px;
    border-radius: 10px;
    text-align: center;
    padding: 5px;
    background-color: rgba(255, 255, 255, 0.9);
    box-shadow: 0 3px 6px rgba(0, 0, 0, 0.16), 0 3px 6px rgba(0, 0, 0, 0.23);
    margin: 0 10px;
    transition: all 0.5s ease;
  }

  .steps:hover {
    transform: scale(1.3);
  }

  strong {
    border-bottom: 1px solid black;
  }
</style>

<div class="info">

  <div class="list">
    <div class="ol-list">

      <div class="steps">
        <strong>Step 1</strong>
        <p>This is a touch screen, you can tap or use the mouse to select</p>
      </div>
      <div class="steps">
        <strong>Step 2</strong>
        <p>
          Click on the Volunteer Name box and start typing to search for your
          name.
        </p>
      </div>
      <div class="steps">
        <strong>Step 3</strong>
        <p>Once you see your name, double click or tap on it to input it.</p>
      </div>
      <div class="steps">
        <strong>Step 4</strong>
        <p>
          Input where you are volunteering at and what you will be doing in the
          Location box.
        </p>
      </div>
      <div class="steps">
        <strong>Step 5</strong>
        <p>
          Press submit. If everything worked correctly, a box will pop up saying
          thanks!
        </p>
      </div>
    </div>

  </div>
  <div class="spans">
    <span>
      &#9654; If you are not volunteering, please use the book to sign in. (ie.
      visiting for lunch, dropping off something, picking up)
    </span>
    <span style="color: red;">
      &#9654; If the visitor is not in the system, use the Guest Visitor name
      and a new input box will come up for the guests name.
    </span>
  </div>
</div>
