<script lang="ts">
import {contributors, totalContributors} from './contributors.ts'
</script>

<h3 style="text-align:center; margin-top:5px; margin-bottom:10px;">Total Contributors {totalContributors}</h3>

<table role="grid" >
  <thead>
    <tr>
      <th scope="col">Name</th>
      <th scope="col">GitHub</th>
    </tr>
  </thead>
  <tbody>
    {#each contributors as contributor}
      <tr>
        <td>{contributor.name}</td>
        <td>
          <a href={contributor.github}>
            {contributor.name}'s Github</a>
        </td>
      </tr>
    {/each}
  </tbody>
</table>



  <style>
  table{
    width:50%;
    margin-left:auto;
    margin-right:auto;
  }
</style>
