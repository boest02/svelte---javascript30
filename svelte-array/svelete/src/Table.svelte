<script>
    export let data = [];
    let headers = [];

    for( var j in data[0] ) {
        headers.push(j);
    } 
</script>

<table>
  <tr> 
    {#each headers as header}
        <th>{header}</th>
    {/each}
  </tr>
  {#each data as item}
    <tr>
        {#each headers as header}
            <td>{item[header]}</td>
        {/each}
    </tr>
  {/each}
</table>


<style>
    table {
        font-family: arial, sans-serif;
        font-size: 20px;
        border-collapse: collapse;
        width: 90%;
        margin: 0 auto;
    }

    th {
        font-weight: bold;
        background: gray;
        text-transform: capitalize;
    }

    td, th {
        border: 1px solid black;
        text-align: left;
        padding: 8px;
        width: 120px;
    }

</style>