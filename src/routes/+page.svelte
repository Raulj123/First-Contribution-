<script lang="ts">
	import { contributors, totalContributors } from './contributors.ts';
</script>

<h3 style="text-align:center; margin-top:5px; margin-bottom:10px;">
	Total Contributors {totalContributors}
	<div class="upper">↑</div>
</h3>
<table role="grid">
	<thead>
		<tr>
			<th scope="col">Name</th>
			<th scope="col">
      <i class="fa-brands fa-github fa-1x"/>
      GitHub</th>
		</tr>
	</thead>
	<tbody>
		{#each contributors as contributor}
			<tr>
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
</style>
