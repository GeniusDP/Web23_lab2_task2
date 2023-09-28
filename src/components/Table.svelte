<!-- Table.svelte -->
<script>
  const VARIANT = 10;
  const WHITE_COLOR = "white";

  let tableData = [];
  let currentColor = WHITE_COLOR;

  // Populate the tableData with numbers from 1 to 36
  for (let i = 1; i <= 6; i++) {
    let row = [];
    for (let j = 1; j <= 6; j++) {
      row.push({
        number: (i - 1) * 6 + j,
        color: WHITE_COLOR,
      });
    }
    tableData.push(row);
  }

  const getRandomColor = () => {
    return '#' + Math.floor(Math.random() * 16777215).toString(16);
  };

  const onMouseDown = (ceilNumber) => {
    variantCeilColorChanger(ceilNumber, getRandomColor()); 
  };

  const onClick = (ceilNumber) => {
    variantCeilColorChanger(ceilNumber, currentColor); 
  };

  const variantCeilColorChanger = (ceilNumber, color) => {
    if (ceilNumber === VARIANT) {
      let newTableData = [];
      for (let i = 0; i < 6; i++) {
        let row = [];
        for (let j = 0; j < 6; j++) {
          row.push({
            number: (i * 6 + j) + 1,
            color: (i * 6 + j) + 1 === VARIANT ? color : tableData[i][j].color,
          });
        }
        newTableData.push(row);
      }
      tableData = newTableData;
    }
  }

  const onDoubleClick = (ceilNumber, rowNumber) => {
    rowColorChanger(ceilNumber, rowNumber); 
  };

  const rowColorChanger = (ceilNumber, rowNumber) => {
    if (ceilNumber === VARIANT) {
      let newTableData = [];
      for (let i = 0; i < 6; i++) {
        let row = [];
        if (i === rowNumber) {
          for (let j = 0; j < 6; j++) {
            row.push({
              number: (i * 6 + j) + 1,
              color: j % 2 == 0 ? getRandomColor() : tableData[i][j].color,
            });
          }
        } else {
          for (let j = 0; j < 6; j++) {
            row.push({
              number: (i * 6 + j) + 1,
              color: tableData[i][j].color,
            });
          }
        }
        newTableData.push(row);
      }
      tableData = newTableData;
    }
  }

</script>

<input type="color" id="color-picker" bind:value={currentColor} />
<table>
  <tbody>
    {#each tableData as row, rowNumber}
      <tr>
        {#each row as { number, color }}
          <td
            style="background-color: {color}"
            on:mouseover={() => onMouseDown(number)}
            on:click={() => onClick(number)}
            on:dblclick={() => onDoubleClick(number, rowNumber)}
          >
            {number}
          </td>
        {/each}
      </tr>
    {/each}
  </tbody>
</table>

<style>
  table {
    border-collapse: collapse;
    width: 50%;
    margin: 0 auto;
  }

  table,
  th,
  td {
    border: 1px solid black;
  }

  th,
  td {
    text-align: center;
    padding: 10px;
  }

  #color-picker {
    width: 250px;
    height: 40px;
  }
</style>
