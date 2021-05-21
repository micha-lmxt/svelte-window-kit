<script>
    import {
        FixedSizeListSSR as List,
        styleString as sty,
        FixedSizeGrid as Grid,
    } from "svelte-window";
    //import List from 'svelte-window/lib/FixedSizeListSSR.svelte'
    //import {styleString as sty} from 'svelte-window/src/styleString'

    let grid;

    const click = () => {
        if (grid) {
            grid.scrollToItem({
                align: "start",
                columnIndex: 150,
                rowIndex: 300,
            });
        }
    };
</script>
<style>
    hr{
        margin:2rem;
    }
</style>
<List height={150} itemCount={1000} itemSize={35} width={300} let:items>
    {#each items || [] as it (it.key)}
        <div style={sty(console.log(it) || it.style)}>Row {it.index}</div>
    {/each}
</List>
<div><hr/></div>

<Grid
  bind:this={grid}
  columnCount={1000}
  columnWidth={150}
  height={250}
  rowCount={1000}
  rowHeight={35}
  width={500}
  useIsScrolling
  let:items>
  {#each items as it (it.key)}
    <div style={sty(it.style)}>
      {it.isScrolling ? 'Scrolling' : `Row ${it.rowIndex} - Col ${it.columnIndex}`}
    </div>
  {/each}
</Grid>

<button on:click={click}> To row 300, column 150 </button>
