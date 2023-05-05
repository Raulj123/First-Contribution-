<script lang="ts">

  let contributors: info[] = [
    {
        name: "Raul",
        github: "https://github.com/Raulj123"
    }
  ]

</script>



<table role="grid" >
  <thead>
    <tr>
      <th scope="col">Name</th>
      <th scope="col">GitHub Username</th>
    </tr>
  </thead>
  {#each contributors as info}
    <tbody>
    <td>{info.name}</td>
    <a href={info.github}>
    <td>{info.name}'s Github</td>
      </a>
    </tbody>
  {/each}
</table>






  <style>
  table{
    width:50%;
    margin-left:auto;
    margin-right:auto;
  }
</style>
