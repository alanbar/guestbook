<script>
    import firebase from "firebase/app" 
    import "firebase/auth"
    import config from './config'

    if(!firebase.apps.length) {
        firebase.initializeApp(config) 
    }

    let user;

    async function login() {
        const result = await firebase.auth().signInWithPopup(new firebase.auth.GoogleAuthProvider())
        user = result.user
        console.log(user)
    }

    async function logout() {
        await firebase.auth().signOut()
        user = null
    }
</script>

<style>
    .profile img.profile {
        height: 50px;
        width: 50px;
        display: block
    }
</style>

{#if user}
<div class="profile">
    <p>{user.displayName}</p>
    <img class="profile" src={user.photoURL} alt="photo"/>
    <button on:click={logout}>Logout</button>
</div>
{:else}
    <button on:click={login}>Login</button>
{/if}