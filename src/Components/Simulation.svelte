<script>
    import { onMount } from 'svelte';
    import * as d3 from 'd3';
  
    let count, index, offset, progress;
  
    // Game state
    let doors = [1, 2, 3];
    let chosenDoor = null;
    let winningDoor = null;
    let hostDoor = null;
    let switched = false;
    let result = null;
    let revealed = false;
    let doorSwitched = false;
  
    // Images
    let doorImage = '/static/door.png';  // Path to the door image in the static directory
    let goatImage = '/static/goat.png';  // Path to the goat image in the static directory
    let carImage = '/static/car.png';    // Path to the car image in the static directory
  
    const chooseDoor = (door) => {
      chosenDoor = door;
      hostDoor = doors.find(d => d !== chosenDoor && d !== winningDoor);
    };
  
    const switchDoor = () => {
      setTimeout(() => {
        chosenDoor = doors.find(d => d !== chosenDoor && d !== hostDoor);
        switched = true;
        doorSwitched = true;
      }, 1000); // 1 second delay
    };
  
    const reveal = () => {
      setTimeout(() => {
        result = chosenDoor === winningDoor ? 'Win' : 'Lose';
        revealed = true;
      }, 1000); // 1 second delay
    };
  
    const resetGame = () => {
      chosenDoor = null;
      winningDoor = doors[Math.floor(Math.random() * doors.length)]; // Randomize winning door
      hostDoor = null;
      switched = false;
      result = null;
      revealed = false;
      doorSwitched = false;
    };
  
    onMount(resetGame);
  </script>
  
  <style>
    .small-visualization {
      width: 80%; /* Adjust width as needed */
      max-width: 500px; /* Set a maximum width if needed */
      margin: 0 auto; /* Center the visualization horizontally */
    }
  
    .section {
      height: 100vh; /* Full height of the viewport */
      overflow-y: auto; /* Enable scrolling within each section */
      display: flex; /* Use flexbox to center content vertically */
      flex-direction: column; /* Stack content vertically */
      justify-content: center; /* Center content horizontally */
      align-items: center; /* Center content vertically */
      text-align: center; /* Center text horizontally */
      padding: 20px; /* Add padding for better readability */
      
      color: black; /* Text color for better readability against gradient */
    }
  
    .section h2 {
      font-size: 2.5rem; /* Larger font size for headings */
    }
  
    .section p {
      font-size: 1.5rem; /* Larger font size for paragraphs */
    }
  
    .doors {
      display: flex;
      justify-content: center;
      gap: 20px;
    }
  
    .door {
      cursor: pointer;
      transition: transform 0.3s; /* Smooth transition for scaling */
    }
  
    .door:hover {
      transform: scale(1.1); /* Slightly enlarge the door on hover */
    }
  
    .chosen {
      transform: scale(1.1); /* Keep the chosen door enlarged */
    }
  
    .door img {
      width: 100px;
      height: 150px;
    }
  
    .hidden {
      display: none;
    }
  
    .buttons {
      margin-top: 20px; /* Add margin to move the buttons below the doors */
    }
  
    #histogram {
      margin-top: 20px; /* Ensures spacing below the text */
    }
  </style>
  
  <div class="section">
    <div>
      <img src="/static/monty.png" alt="Monty Hall" style="width: 500px; height: auto;" />
      <h2>Welcome to the Monty Hall Problem!</h2>
    </div>
    <div class="content">
      <p>The Monty Hall problem is a brain teaser, in the form of a probability puzzle, 
        based nominally on the American television game show Let's Make a Deal and named 
        after its original host, Monty Hall.</p>
      <p>Suppose you're on a game show, and you're given the choice of three doors: 
        Behind one door is a car; behind the others, goats. You pick a door, say No. 1, 
        and the host, who knows what's behind the doors, opens another door, say No. 3, 
        which has a goat. He then says to you, "Do you want to pick door No. 2?" Is it to
        your advantage to switch your choice?</p>
    </div>
  </div>
  
  <div class="section">
    <div>
      <h2>Iteration of the Game</h2>
    </div>
    <div class="content">
      {#if !chosenDoor}
        <p>Choose a door:</p>
        <div class="doors">
          {#each doors as door}
            <div class="door" on:click={() => chooseDoor(door)}>
              <img src={doorImage} alt={`Door ${door}`} />
            </div>
          {/each}
        </div>
      {:else if !result}
        <p>Host opens door {hostDoor}.</p>
        <div class="doors">
          {#each doors as door}
            <div class="door {chosenDoor === door ? 'chosen' : ''}" on:click={() => chosenDoor === door && !revealed ? reveal() : null}>
              {#if door === hostDoor}
                <img src={goatImage} alt="Goat" />
              {:else if revealed && door === chosenDoor}
                <img src={door === winningDoor ? carImage : goatImage} alt={door === winningDoor ? 'Car' : 'Goat'} />
              {:else}
                <img src={doorImage} alt={`Door ${door}`} />
              {/if}
            </div>
          {/each}
        </div>
        <div class="buttons">
          {#if !doorSwitched}
            <button on:click={switchDoor}>Switch Door</button>
          {/if}
          <button on:click={reveal}>Reveal</button>
        </div>
      {:else}
        <p>You {result}!</p>
        <div class="doors">
          {#each doors as door}
            <div class="door {chosenDoor === door ? 'chosen' : ''}">
              {#if door === chosenDoor}
                <img src={door === winningDoor ? carImage : goatImage} alt={door === winningDoor ? 'Car' : 'Goat'} />
              {:else if door === hostDoor}
                <img src={goatImage} alt="Goat" />
              {:else}
                <img src={door === winningDoor ? carImage : goatImage} alt={door === winningDoor ? 'Car' : 'Goat'} />
              {/if}
            </div>
          {/each}
        </div>
        <div class="buttons">
          <button on:click={resetGame}>Play Again</button>
        </div>
      {/if}
    </div>
  </div>