<script>
  const symbols = 'C CE % / 7 8 9 * 4 5 6 - 1 2 3 + 0 ( ) ='.split(' ');
  let tablo = 'tablo';

  /**
   * @param {string} key
   */
  function handleClick(key) {
    if (key.match(/=|Enter/)) {
      try {
        tablo = eval(tablo);
      } catch {
        let oldValue = tablo;
        let newValue = 'недопустимое выражение';
        tablo = newValue;
        setTimeout(() => {
          tablo = oldValue;
        }, 1500);
      }
    } else if (key === 'C') {
      tablo = '';
    } else if (key.match(/CE|Backspace/)) {
      tablo = tablo.substring(0, tablo.length - 1);
    } else {
      tablo += key;
    }
  }
</script>

<svelte:window
  on:keypress={(e) => {
    if (e.key.match(/[0-9%\/*\-+\(\)=]|Backspace|Enter/)) {
      handleClick(e.key);
    }
  }}
/>

<main>
  <div class="calculator">
    <output>{tablo}</output>
    {#each symbols as symbol}
      <button on:click={() => handleClick(symbol)}>{symbol}</button>
    {/each}
  </div>
</main>

<style>
  .calculator {
    display: grid;
    grid-template-columns: repeat(4, auto);
    gap: 10px;
  }
  output {
    grid-row: 1px;
    grid-column: 1 / -1;
    min-height: 1.5em;
  }
</style>
