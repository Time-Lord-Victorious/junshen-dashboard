<script>
    import supabase from '$lib/db';
import Navbar from '$lib/Navbar.svelte';
    async function logout() {
   	 const { error } = await supabase.auth.signOut();

   	 if (error) alert(error.message); // alert if error
    }
	let episodeList = [
		{
			name: "Doctor Who: Inferno from Space",
			part: 1,
			author: "Junshen",
			date: "1st of May 8pm"
		},
		{
			name: "Doctor Who: Inferno from Space",
			part: 2,
			author: "Junshen",
			date: "15th of May 8pm" 
		}
	]
	function addEpisode(){
		episodeList = [
    ...episodeList,
    { name: "??", part: 1, author: "", date: ""}
  ];
	}
</script>
<Navbar/>

	<div class="container mt-5">
		<table class="table">
		<thead>
		  <tr>
			<th scope="col">Epsiode name</th>
			<th scope="col">Part No.</th>
			<th scope="col">Written by:</th>
			<th scope="col">Release</th>
		  </tr>
		</thead>
		<tbody>
		{#each episodeList as episode}
		<tr>
			<td>{episode.name}</td>
			<td>{episode.part}</td>
			<td>{episode.author}</td>
			<td>{episode.date}</td>
		  </tr>
		{/each}
		<tr>
			<td><button class="btn btn-success" type="button" on:click={addEpisode}>+</button></td>
		</tr>
		</tbody>
  </table>
</div>
<!-- Sign Out -->
<section class="container px-4 py-3 text-center">
    <button class="btn btn-secondary" on:click={logout}>Logout</button>
</section>		
