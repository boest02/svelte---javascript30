<script>
    export let data = {};
    
</script>

<div>
    {JSON.stringify(data, null, 2)}
</div>

<style>
    div {
        font-family: arial, sans-serif;
        font-size: 20px;
        border-collapse: collapse;
        width: 80%;
        margin: 0 auto;
        padding: 15px;
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