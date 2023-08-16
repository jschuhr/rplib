<!-- src/routes/signup.svelte -->
<script>
    //import { supabase } from '../lib/supabaseClient';
    import { supabase } from "$lib/supabaseClient";


    let email = '';
    let password = '';
    let confirmPassword = '';
    // @ts-ignore
    /**
	 * @type {string | null}
	 */
    let error = null;

    async function signup() {
        if (password !== confirmPassword) {
            error = "Passwords do not match!";
            return;
        }

        try {
            const { data, error: signupError } = await supabase.auth.signUp({ email, password });
            if (signupError) throw signupError;

            // You can send a confirmation email or redirect to a thank you page.
            // For now, let's just log the user data.
            console.log(data);
        } catch (err) {
            // @ts-ignore
            error = err.message;
        }
    }
</script>

<main>
    <h1>Signup</h1>
    
    <form on:submit|preventDefault={signup}>
        <div>
            <label for="email">Email:</label>
            <input type="email" id="email" bind:value={email} required>
        </div>
        
        <div>
            <label for="password">Password:</label>
            <input type="password" id="password" bind:value={password} required>
        </div>

        <div>
            <label for="confirmPassword">Confirm Password:</label>
            <input type="password" id="confirmPassword" bind:value={confirmPassword} required>
        </div>

        {#if error}
            <div class="error">
                {error}
            </div>
        {/if}

        <button class="btn variant-filled" type="submit">Signup</button>
    </form>
</main>

<style>
    /* Add your styles here. For instance: */
    .error {
        color: red;
    }
</style>
