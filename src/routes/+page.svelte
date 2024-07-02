<script>
  import { onMount } from 'svelte';

  const colors = [
    "#e9b872",
    "#d66853",
    "#6b9ac4",
    "#000000",
    "ffffff"
  ];

  function shuffleArray(array) {
    return array.slice().sort(() => Math.random() - 0.5);
  }

  function generateColorSequence() {
    const shuffled = shuffleArray(colors);
    return shuffled.join(';') + ';' + shuffled[0];
  }

  let colorSequences = Array(6).fill('').map(() => generateColorSequence());

  onMount(() => {
    // Regenerate color sequences periodically if desired
    const interval = setInterval(() => {
      colorSequences = colorSequences.map(() => generateColorSequence());
    }, 20000); // Change every 20 seconds

    return () => clearInterval(interval);
  });

  let name = '';
  let email = '';

  function handleSubmit() {
    // Handle form submission
    console.log('Name:', name);
    console.log('Email:', email);
    // Reset form fields
    name = '';
    email = '';
  }
</script>

<div class="container">
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 300 400">   
    {#each colorSequences as sequence, rowIndex}
      <g transform="translate(0, {rowIndex * 50})">
        {#each [25, 75, 125, 175, 225, 275] as cx, index}
          <circle {cx} cy="25" r="20">
            <animate attributeName="fill" values={sequence} dur="2s" repeatCount="indefinite" begin={`${index * 1}s`}/>
          </circle>
        {/each}
      </g>
    {/each}
    
    <text x="0" y="380" font-family="Arial, sans-serif" font-size="24" font-weight="bold" textLength="180px">OPEN MIC</text>
    <text x="220" y="380" font-family="Arial, sans-serif" font-size="24" font-weight="bold" textLength="80px">08/28</text>
  </svg>

  <div class="form-container">
    <form on:submit|preventDefault={handleSubmit}>
      <input type="text" id="name" placeholder="NAME" bind:value={name} required>
      <input type="email" placeholder="EMAIL" id="email" bind:value={email} required>
      <button type="submit">SIGN UP</button>
    </form>
  </div>
</div>

<style>
  .container {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    max-width: 800px;
    max-height: 100vh;
    margin: 0 auto;
  }

  .form-container {
    margin: 20px;
  }

  form {
    display: flex;
    flex-direction: column;
  }

  input {
    margin-bottom: 10px;
    padding-left: 100px;
    padding-right: 100px;
    padding-top: 10px;
    padding-bottom: 10px;
    border-radius: 10px;
    text-align: center;
    background-color: inherit;
    border-width: 1px;
    border-color: black;

  }

  button {
    padding: 10px;
    border-radius: 10px;
    font-weight: bold;
    background: inherit;
    border-width: 1px;
    border-color: black;
    letter-spacing: 4px;
  }
</style>