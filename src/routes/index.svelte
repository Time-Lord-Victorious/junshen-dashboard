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
			<th scope="col">Release</th>
		  </tr>
		</thead>
		<tbody>
		  <tr>
			<th scope="row">1</th>
			<td>Doctor Who: Inferno from Space</td>
			<td>Part 1</td>
			<td>Junshen</td>
			<td>1st of May 8pm</td>
		  </tr>
		  <tr>
			<th scope="row">2</th>
			<td>Doctor Who: Inferno from Space</td>
			<td>Part 2</td>
			<td>Junshen</td>
			<td>15th of May 8pm</td>
		  </tr>
		  <tr>
			<th scope="row">3</th>
			<td>Doctor Who: Peace and War</td>
			<td>Part 1</td>
			<td>Junshen</td>
			<td>1st of June 8pm</td>
		  </tr>
		  <tr>
			<th scope="row">4</th>
			<td>Doctor Who: Peace and War</td>
			<td>Part 2</td>
			<td>Jun Shen Lee</td>
			<td>15th of June 8pm</td>
		  </tr>
		  <tr>
			<th scope="row">5</th>
			<td>The Ip Man Adventures 1</td>
			<td>Part 1</td>
			<td>Junshen</td>
			<td>1st of July 8pm</td>
		  </tr>
		  <tr>
		  <th scope="row">5</th>
			<td>The Ip Man Adventures 1</td>
			<td>Part 2</td>
			<td>Junshen</td>
			<td>15th of July 8pm</td>
		  </tr>
		  <tr>
			<th scope="row">6</th>
			<td>The Ip Man Adventures 2</td>
			<td>Part 1</td>
			<td>Junshen</td>
			<td>1st of August 8pm</td>
		  </tr>
		  <tr>
			<th scope="row">7</th>
			<td>The Ip Man Adventures 2</td>
			<td>Part 2</td>
			<td>Junshen</td>
			<td>15th of August 8pm</td>
		  </tr>
		  <tr>
			<th scope="row">8</th>
			<td>The Ip Man Adventures 3</td>
			<td>Part 1</td>
			<td>Junshen</td>
			<td>1st of September 8pm</td>
		  </tr>
		  <tr>
			<th scope="row">8</th>
			<td>The Ip Man Adventures 3</td>
			<td>Part 2</td>
			<td>Junshen</td>
			<td>15th of September 8pm</td>
		  </tr>
		</tbody>
  </table>
</div>
<!-- Sign Out -->
<section class="container px-4 py-3 text-center">
    <button class="btn btn-secondary" on:click={logout}>Logout</button>
</section>		
