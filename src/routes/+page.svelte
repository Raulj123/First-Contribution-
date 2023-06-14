<script lang="ts">
	import { contributors, totalContributors } from './contributors.ts';
function getUsernameFromUrl(url: string): string | null {
  const urlObj = new URL(url);
  const pathParts = urlObj.pathname.split('/');

  // The username is typically the second part of the path
  if (pathParts.length >= 2) {
    const username = pathParts[1];
    console.log('Extracted username:', username);
    return `https://avatars.githubusercontent.com/${username}`;
    } else {
    console.error('Invalid GitHub profile URL');
    return null;
  }
}


</script>

<h3 style="text-align:center; margin-top:5px; margin-bottom:10px;">
	Total Contributors {totalContributors}
	<div class="upper">↑</div>
</h3>
<table role="grid">
	<thead>
		<tr>
      <th scope="col">Avatar</th>
			<th scope="col">Name</th>
					
      <th scope="col">
      <i class="fa-brands fa-github fa-1x"/>
        GitHub
      </th> 

		</tr>
	</thead>
	<tbody>
		{#each contributors as contributor}
			<tr>
         <td>
        <img src="{getUsernameFromUrl(contributor.github)}" alt="{contributor.name}'s Avatar">
      </td>
				<td>{contributor.name}</td>
				<td>
					<a href={contributor.github}> {contributor.name}'s Github</a>
				</td>
			</tr>
		{/each}
	</tbody>
</table>

<style>
	table {
		width: 50%;
		margin-left: auto;
		margin-right: auto;
	}
	.upper {
		display: inline-block;
		color: green;
		animation: upper-to 1000ms ease-in-out infinite;
	}
	@keyframes upper-to {
		0% {
			transform: translateY(0px);
		}
		100% {
			transform: translateY(-5px);
		}
	}
  tbody tr:hover {
  border: 2px solid blue;
  border-color: hsl(195, 85%, 41%);
  }
  img {
    width: 45px;
    height: 45px;
    border-radius:10px;
  }

</style>
