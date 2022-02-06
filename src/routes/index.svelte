<script>
    import supabase from '$lib/db';
import Navbar from '$lib/Navbar.svelte';
    async function logout() {
   	 const { error } = await supabase.auth.signOut();

   	 if (error) alert(error.message); // alert if error
    }
	
</script>
<Navbar/>

	<div class="container mt-5">
		<table class="table">
		<thead>
		  <tr>
			<th scope="col">#</th>
			<th scope="col">First</th>
			<th scope="col">Last</th>
			<th scope="col">Handle</th>
		  </tr>
		</thead>
		<tbody>
		  <tr>
			<th scope="row">1</th>
			<td>Mark</td>
			<td>Otto</td>
			<td>@mdo</td>
		  </tr>
		  <tr>
			<th scope="row">2</th>
			<td>Jacob</td>
			<td>Thornton</td>
			<td>@fat</td>
		  </tr>
		  <tr>
			<th scope="row">3</th>
			<td colspan="2">Larry the Bird</td>
			<td>@twitter</td>
		  </tr>
		</tbody>
  </table>
</div>
<!-- Sign Out -->
<section class="container px-4 py-3 text-center">
    <button class="btn btn-secondary" on:click={logout}>Logout</button>
</section>		
