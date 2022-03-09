<script>
    import supabase from '$lib/db';
	import Navbar from './Navbar.svelte'; 
    
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
		},
		{
			name: "Doctor Who: Peace and War",
			part: 1,
			author: "Junshen",
			date: "1st of June 8pm" 
		},
		{
			name: "Doctor Who: Peace and War",
			part: 2,
			author: "Junshen",
			date: "15th of June 8pm" 
		},
	]
	
	function addEpisodeDetails(){
		episodeList = [...episodeList,{name: "??", part: 1, author: "", date: ""}];
	}

	let curName;
	let curPart;
	let curAuthor;
	let curDate;
	let curIndex;

	function showEpisodeDetails(index,name,part,author,date){
		curIndex=index;
		curName=name;
		curPart=part;
		curAuthor=author;
		curDate=date;
		console.log(curName);
	}

// Upsert entry
async function saveEntry() {
  const { error } = await supabase.from("episodeEntries").upsert(
    {
      user_id: supabase.auth.user().id,
      detailsTable: episodeList,
    },
    { onConflict: "user_id" }
  );
  if (error) alert(error.message);
}
function setepisodeDetails(index, newName, newPart, newAuthor, newDate){

	episodeList[index].name = newName
	episodeList[index].part = newPart
	episodeList[index].author = newAuthor
	episodeList[index].date = newDate

	saveEntry();
};
	function deleteEpisodeDetails(index){
		episodeList.splice(index,1);
		episodeList=episodeList;
		saveEntry();
	}
	
	// Get entries
async function getEntries() {
  const { data, error } = await supabase.from("episodeEntries").select();
  if (error) alert(error.message);

  if (data != "") {
    episodeList = data[0].detailsTable;
  }
}

getEntries();
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
			<th scope="col">Action</th>
		  </tr>
		</thead>
		<tbody>
		{#each episodeList as episode,index}
		<tr>
			<td>{episode.name}</td>
			<td>{episode.part}</td>
			<td>{episode.author}</td>
			<td>{episode.date}</td>
			<td>
				<button data-bs-toggle="modal" data-bs-target="#editRow" on:click={() =>
					showEpisodeDetails(
					 index,
					  episode.name,
					  episode.part,
					  episode.author,
					  episode.date
					)}>Edit</button>
				<button data-bs-toggle="modal" data-bs-target="#deleteRow" on:click={()=>{curIndex=index;}}>Delete</button>
			</td>
		  </tr>
		{/each}
		</tbody>
  </table>
</div>

<!-- Add 1 more row for episode -->
<section class="container text-center mb-2">
    <button class="btn btn-success" on:click={addEpisodeDetails}>Add Episode</button>
</section>	

<!-- Sign Out -->
<section class="container text-center">
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
		  <button type="button" class="btn btn-danger">Delete</button>
		  <button type="button" class="btn btn-primary">Save changes</button>
		</div>
	  </div>
	</div>
  </div>
  
 <!-- Modal box for Edit -->
 <div class="modal fade" id="editRow" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
	<div class="modal-dialog">
	  <div class="modal-content">
		<div class="modal-header">
		  <h5 class="modal-title" id="exampleModalLabel">Edit Information</h5>
		  <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
		</div>
		<div class="modal-body">
			<div class="input-group mb-3">
				<span class="input-group-text w-25" id="basic-addon1">Ep Name</span>
				<input type="text" class="form-control" placeholder="Episode Name" aria-label="Episode Name" aria-describedby="basic-addon1" bind:value={curName}>
			</div>
			<div class="input-group mb-3">
				<span class="input-group-text w-25" id="basic-addon1">Part</span>
				<input type="text" class="form-control" placeholder="Part" aria-label="Part" aria-describedby="basic-addon1" bind:value={curPart}>
			</div>
			<div class="input-group mb-3">
				<span class="input-group-text w-25" id="basic-addon1">Written by</span>
				<input type="text" class="form-control" placeholder="Author" aria-label="Author" aria-describedby="basic-addon1" bind:value={curAuthor}>
			</div>
			<div class="input-group mb-3">
				<span class="input-group-text w-25" id="basic-addon1">Release Date</span>
				<input type="text" class="form-control" placeholder="Release Date" aria-label="Release Date" aria-describedby="basic-addon1" bind:value={curDate}>
			</div>

		</div>
		<div class="modal-footer">
		  <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
		  <button type="button" class="btn btn-primary" on:click={()=>{setepisodeDetails(curIndex, curName, curPart, curAuthor, curDate)}} data-bs-dismiss="modal">Save changes</button>
		</div>
	  </div>
	</div>
  </div>

   <!-- Modal box for Delete row -->
   <div class="modal fade" id="deleteRow" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
	  <div class="modal-dialog">
		<div class="modal-content">
		  <div class="modal-header">
			<h5 class="modal-title" id="exampleModalLabel">Delete Information</h5>
			<button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
		  </div>
		  <div class="modal-body">
				<p>Are you sure you would like to delete this episode?</p>
		  </div>
		  <div class="modal-footer">
			<button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
			<button type="button" class="btn btn-danger" data-bs-dismiss="modal" on:click={()=>{
				deleteEpisodeDetails(curIndex);
			}}>Delete</button>
		  </div>
		</div>
	  </div>
	</div>
  


