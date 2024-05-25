<script>
	import { onMount } from 'svelte';
  
	let data = [];
  
	async function fetchData() {
	  try {
		const response = await fetch('/perspective-plan.json');
		data = await response.json();
	  } catch (error) {
		console.error('Error:', error);
	  }
	}
  
	onMount(fetchData);
  </script>
  
  <style>
	@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700&display=swap');
  
	body {
	  font-family: 'Montserrat', sans-serif;
	  background-color: #f6f6ff;
	  color: #020508;
	}
  
	.card {
	  background-color: #f3f7fd;
	  color: #111417;
	}
  </style>
  
  <svelte:head>
	<title>Perspective Plan</title>
	<link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
  </svelte:head>
  
  <h1 class="h-20 flex items-center justify-center bg-gray-900 text-gray-200 text-3xl">PERSPECTIVE PLAN</h1>
  <div class="container mx-auto px-4 py-8">
	<div class="grid grid-cols-1 gap-4">
	  {#each data as item}
		<div class="card rounded-lg shadow-md p-4">
		  <h2 class="text-lg font-semibold mb-2">{item.name}</h2>
		  {#if item.responsibility}
			<p class="text-gray-700 mb-1">Responsibility: <span>{item.responsibility}</span></p>
		  {/if}
		  {#if item.rank}
			<p class="text-gray-700 mb-1">Rank: <span>{item.rank}</span></p>
		  {/if}
		  {#if item.children}
			<div class="ml-4 grid grid-cols-1 gap-4">
			  {#each item.children as child}
				<div class="card rounded-lg shadow-md p-4">
				  <h2 class="text-lg font-semibold mb-2">{child.name}</h2>
				  {#if child.responsibility}
					<p class="text-gray-700 mb-1">Responsibility: <span>{child.responsibility}</span></p>
				  {/if}
				  <!-- {#if child.rank}
					<p class="text-gray-700 mb-1">Rank: <span>{child.rank}</span></p>
				  {/if} -->
				</div>
			  {/each}
			</div>
		  {/if}
		</div>
	  {/each}
	</div>
  </div>
  