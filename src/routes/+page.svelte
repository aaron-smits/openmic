<script>
  import { onMount } from 'svelte';

  const colors = [
    "#e9b872",
    "#d66853",
    "#6b9ac4",
    "#000000"
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
</script>

<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 300 400">
  <rect width="100%" height="100%"/>
  
  {#each colorSequences as sequence, rowIndex}
    <g transform="translate(0, {rowIndex * 50})">
      {#each [25, 75, 125, 175, 225, 275] as cx, index}
        <circle {cx} cy="25" r="20">
          <animate attributeName="fill" values={sequence} dur="4s" repeatCount="indefinite" begin={`${index * 0.5}s`}/>
        </circle>
      {/each}
    </g>
  {/each}
  
  <text x="20" y="380" font-family="Arial, sans-serif" font-size="24" font-weight="bold">OPEN MIC</text>
  <text x="220" y="380" font-family="Arial, sans-serif" font-size="24" font-weight="bold">08/28</text>
</svg>