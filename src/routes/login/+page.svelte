
<script>
    import { supabase } from "$lib/supabaseClient";


    let email = '';
    let password = '';
    /**
	 * @type {null}
	 */
    let error = null;

    async function login() {
        try {
            const { data, error: loginError } = await supabase.auth.signInWithPassword({ email, password });
            if (loginError) throw loginError;

            // Redirect to a protected route after successful login or any other action.
            // For now, we will just console log the user data.
            console.log(data);
        } catch (err) {
            // @ts-ignore
            error = err.message;
        }
    }
</script>

<main>
    <h1>Login</h1>
    
    <form on:submit|preventDefault={login}>
        <div>
            <label for="email">Email:</label>
            <input class="input" type="email" id="email" bind:value={email} required>
        </div>
        
        <div>
            <label for="password" class="label">Password:</label>
            <input class="input" type="password" id="password" bind:value={password} required>
        </div>

        {#if error}
            <div class="error">
                {error}
            </div>
        {/if}

        <button type="submit" class="btn variant-filled">Login</button>
    </form>
</main>

<style>
    /* Add your styles here. For instance: */
    .error {
        color: red;
    }
</style>
