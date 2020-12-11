<script>

	import {gameState} from './store';
	import {gameClient} from './GameClient'

	const onClick = (id) => {
		gameClient.client.moves.clickCell(id);
	};


	$:{ console.log($gameState)}

</script>

<style>
	.cell {
		border: 1px solid #555;
		width: 50px;
		height: 50px;
		line-height: 50px;
		text-align: center;
	}
</style>

<div>
	{#if $gameState && $gameState.G}
	<table id="board">
		<tbody>
			{#each [0, 1, 2] as i}
				<tr>
					{#each [0, 1, 2] as j}
						<td class="cell" on:click={() => onClick(3 * i + j)}>
							{$gameState.G.cells[3 * i + j] || ''}
						</td>
					{/each}
				</tr>
			{/each}
		</tbody>
	</table>
	{/if}
	{#if $gameState.ctx.gameover}
	<div id="winner">
		{$gameState.ctx.gameover.winner!== undefined 
		? `Winner ${$gameState.ctx.gameover.winner}`
		: "Draw!" }
	</div>
	{/if}

	
</div>
