<script> 
    import supabase from '$lib/db';
    import { page, session } from '$app/stores';
    import { browser } from '$app/env';
    import { goto } from '$app/navigation';

    // code will only run in the browser
    if (browser) {
       // set session on page loaded
   	 $session = supabase.auth.session(); // set session
   	 redirect();

       // code will run whenever logout or login
   	 supabase.auth.onAuthStateChange((event, userSession) => {
   		 $session = userSession; // set session
   		 redirect();
   	 });
    }

    function redirect() {
   	 // login redirect
   	 if ($session && $page.url.pathname === '/login') {
   		 goto('/');
   	 }

   	 // logout redirect
   	 if (!$session && $page.url.pathname === '/') {
   		 goto('/login');
   	 }
    }
</script>
<slot />