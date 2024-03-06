<style>
  .row {
    margin: 0 0 25px;
    display: flex;
    gap: 25px;
    background-color: #f000;
    width: fit-content;
  }
  .item {
    background-color: #f004;
    height: 50px;
    font-size: 15px;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 50px;
  }
  
  table {
    margin-top: 50px;
    font-size: 15px;
    background-color: #f002;
  }
  td {
    background-color: #f002;
    padding: 5px 25px 5px 5px;
  }
  </style>

<script lang="ts">
  let total = 100
  let maxRowLength = 10

  let previousRowLength = 0;
  let currentRowLength = 0;
  let currentRowIndex = 0
  let startDecreasing = false;

  function generateRows() {
    let result: number[][] = []
    Array.from({length: total}).forEach((_, itemIndex) => {
      const label = itemIndex + 1;

      
      if(currentRowLength === 0) {
        result.push([label])
        currentRowLength = 1
      } else {
        result[currentRowIndex].push(label)
        currentRowLength++
      }

      if(currentRowLength === maxRowLength) {
        startDecreasing = true;
      }
      
      const startNewRow = startDecreasing 
        ? currentRowLength + 2 > previousRowLength 
        : currentRowLength > previousRowLength;

      if(startNewRow) {
        previousRowLength = currentRowLength
        currentRowLength = 0
        currentRowIndex++
      }

      if(previousRowLength === 1 && startNewRow) {
        startDecreasing = false
      }
    })
    return result;
  }
  let rows = generateRows();
</script>

{#each rows as row}
  <div class="row">
    {#each row as item}
      <span class="item">{item}</span>
    {/each}  
  </div>
  
{/each}