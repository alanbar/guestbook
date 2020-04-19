<script>
    import firebase from "firebase/app" 
    import "firebase/auth"
    import config from './firebase/config'
    import Guestbook from  "./firebase/Guestbook.svelte"
    import Profile from  "./firebase/Profile.svelte"

    if(!firebase.apps.length) {
        firebase.initializeApp(config) 
    }

    let user;

    async function login() {
        const result = await firebase.auth().signInWithPopup(new firebase.auth.GoogleAuthProvider())
        user = result.user
       // console.log('u', user)
    }

    async function logout() {
        await firebase.auth().signOut()
        user = null
    }
</script>

{#if user}
    <Profile {...user} />
    <p></p>
    <button on:click={logout}>Logout</button>
    <p></p>
    <Guestbook />

{:else}
    <button on:click={login}>Login</button>
{/if}

