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
			<td>
				<button data-bs-toggle="modal" data-bs-target="#editTitle">{episode.name}</button></td>
			<td><button data-bs-toggle="modal" data-bs-target="#editPart">{episode.part}</button></td>
			<td><button data-bs-toggle="modal" data-bs-target="#editAuthor">{episode.author}</button></td>
			<td><button data-bs-toggle="modal" data-bs-target="#editDate">{episode.date}</button></td>
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
    <button class="btn btn-primary" on:click={logout}>Logout</button>
</section>		

  <!-- Modal -->
<div class="modal fade" id="editTitle" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
	<div class="modal-dialog">
	  <div class="modal-content">
		<div class="modal-header">
		  <h5 class="modal-title" id="exampleModalLabel">Edit Information</h5>
		  <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
		</div>
		<div class="modal-body">
			<div class="input-group mb-3">
				<span class="input-group-text" id="basic-addon1">New title</span>
				<input type="text" class="form-control" placeholder="New Title" aria-label="New Title" aria-describedby="basic-addon1">
			  </div>
		</div>
		<div class="modal-footer">
		  <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
		  <button type="button" class="btn btn-primary">Save changes</button>
		</div>
	  </div>
	</div>
  </div>
  
 <!-- Modal -->
 <div class="modal fade" id="editPart" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
	<div class="modal-dialog">
	  <div class="modal-content">
		<div class="modal-header">
		  <h5 class="modal-title" id="exampleModalLabel">Edit Information</h5>
		  <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
		</div>
		<div class="modal-body">
			<div class="input-group mb-3">
				<span class="input-group-text" id="basic-addon1">New Part</span>
				<input type="text" class="form-control" placeholder="New Part" aria-label="New Part" aria-describedby="basic-addon1">
			  </div>
		</div>
		<div class="modal-footer">
		  <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
		  <button type="button" class="btn btn-primary">Save changes</button>
		</div>
	  </div>
	</div>
  </div>

   <!-- Modal -->
<div class="modal fade" id="editAuthor" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
	<div class="modal-dialog">
	  <div class="modal-content">
		<div class="modal-header">
		  <h5 class="modal-title" id="exampleModalLabel">Edit Information</h5>
		  <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
		</div>
		<div class="modal-body">
			<div class="input-group mb-3">
				<span class="input-group-text" id="basic-addon1">New Author</span>
				<input type="text" class="form-control" placeholder="New Author" aria-label="New Author" aria-describedby="basic-addon1">
			  </div>
		</div>
		<div class="modal-footer">
		  <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
		  <button type="button" class="btn btn-primary">Save changes</button>
		</div>
	  </div>
	</div>
  </div>

   <!-- Modal -->
<div class="modal fade" id="editDate" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
	<div class="modal-dialog">
	  <div class="modal-content">
		<div class="modal-header">
		  <h5 class="modal-title" id="exampleModalLabel">Edit Information</h5>
		  <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
		</div>
		<div class="modal-body">
			<div class="input-group mb-3">
				<span class="input-group-text" id="basic-addon1">New Date</span>
				<input type="text" class="form-control" placeholder="New Date" aria-label="New Date" aria-describedby="basic-addon1">
			  </div>
		</div>
		<div class="modal-footer">
		  <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
		  <button type="button" class="btn btn-primary">Save changes</button>
		</div>
	  </div>
	</div>
  </div>