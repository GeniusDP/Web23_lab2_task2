<script>
  import Table from "./components/Table.svelte";
</script>

<main>
  <h1>6x6 Table with Numbers 1-36</h1>
  <Table />
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }

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
</style>
