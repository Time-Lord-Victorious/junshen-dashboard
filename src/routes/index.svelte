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
			<th scope="col">Episode No.</th>
			<th scope="col">Epsiode name</th>
			<th scope="col">Part No.</th>
			<th scope="col">Written by:</th>
		  </tr>
		</thead>
		<tbody>
		  <tr>
			<th scope="row">1</th>
			<td>Doctor Who: Inferno from Space</td>
			<td>Part 1</td>
			<td>Jun Shen Lee</td>
		  </tr>
		  <tr>
			<th scope="row">2</th>
			<td>Doctor Who: Inferno from Space</td>
			<td>Part 2</td>
			<td>Jun Shen Lee</td>
		  </tr>
		  <tr>
			<th scope="row">3</th>
			<td>Doctor Who: the Grandmaster</td>
			<td>Part 1</td>
			<td>Jun Shen Lee</td>
		  </tr>
		  <tr>
			<th scope="row">4</th>
			<td>Doctor Who: the Grandmaster</td>
			<td>Part 2</td>
			<td>Jun Shen Lee</td>
		  </tr>
		  <tr>
			<th scope="row">5</th>
			<td>Doctor Who: The Plant</td>
			<td>Full episode</td>
			<td>Jun Shen Lee</td>
		  </tr>
		  <tr>
			<th scope="row">6</th>
			<td>Doctor Who: The Sontaran Gambit</td>
			<td>Part 1</td>
			<td>Jun Shen Lee</td>
		  </tr>
		  <tr>
		  <th scope="row">7</th>
			<td>Doctor Who: The Sontaran Gambit</td>
			<td>Part 2</td>
			<td>Jun Shen Lee</td>
		  </tr>
		  <tr>
			<th scope="row">8</th>
			<td>Doctor Who: The 6 Doctors</td>
			<td>Part 1</td>
			<td>Jun Shen Lee</td>
		  </tr>
		  <tr>
			<th scope="row">9</th>
			<td>Doctor Who: The 6 Doctors</td>
			<td>Part 2</td>
			<td>Jun Shen Lee</td>
		  </tr>
		  <tr>
			<th scope="row">8</th>
			<td>Doctor Who: The 6 Doctors</td>
			<td>Part 3</td>
			<td>Jun Shen Lee</td>
		  </tr>
		</tbody>
  </table>
</div>
<!-- Sign Out -->
<section class="container px-4 py-3 text-center">
    <button class="btn btn-secondary" on:click={logout}>Logout</button>
</section>		
