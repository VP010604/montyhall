<script>
  import katexify from "../katexify";
</script>

<section id = "body">
<h1 class="body-header">The Math of The Monty Hall Problem</h1>
<p class="body-text">
  Suppose you're on a game show, and you're given the choice of three doors:
  Behind one door is a car; behind the others, goats. You pick a door, say No. 1,
  and the host, who knows what's behind the doors, opens another door, say No. 3, 
  which has a goat. He then says to you, "Do you want to pick door No. 2?" Is it to your 
  advantage to switch your choice?
</p>
<p class="body-text">
  When the player first makes their choice, there is a 
2
/
3
 chance that the car is behind one of the doors not chosen. This probability does not change after the host reveals a goat behind one of the unchosen doors. When the host provides information about the two unchosen doors (revealing that one of them does not have the car behind it), the 
2
/
3
 chance of the car being behind one of the unchosen doors rests on the unchosen and unrevealed door, as opposed to the 
1
/
3
 chance of the car being behind the door the contestant chose initially.
</p>
</section>

<style>
  #body {
    max-width: 600px;
    margin: 1rem auto;
    text-align: center;
    padding-top: 1rem;
  }

  .body-header {
    font-size: 2rem;
    margin-top: 5px;
    margin-bottom: 0;
    letter-spacing: 1.5px;
    text-transform: uppercase;
    max-width: 100%;
    margin: auto;
    text-align: center;
    color: black;
    font-family: 'Times New Roman', Times, serif;
  }

  .body-text {
    font-size: 1.4rem;
    color: black;
    text-align: center;
    margin: 1rem;
    opacity: 0.75;
    padding: 2rem;
    font-family: 'Times New Roman', Times, serif;
  }
</style>
