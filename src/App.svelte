<script>
	 import {Router, Link, Route,navigate} from "svelte-routing"
	 //import { firebaseui } from "firebase/auth";
	import Login from "./pages/Login.svelte";
	import Logout from "./pages/Logout.svelte";
	import Home from "./pages/Home.svelte";
	import FileUpload from "./pages/FileUpload.svelte";
	import { initializeApp } from "firebase/app";
	import { getAuth,onAuthStateChanged } from "firebase/auth";


	const firebaseConfig = {
        apiKey: "AIzaSyCAG4T5zJpZT0jLzcQtxxTEIwlsuE53JVs",
  authDomain: "svelte-cf13d.firebaseapp.com",
  databaseURL: "https://svelte-cf13d-default-rtdb.asia-southeast1.firebasedatabase.app",
  projectId: "svelte-cf13d",
  storageBucket: "svelte-cf13d.appspot.com",
  messagingSenderId: "686433020439",
  appId: "1:686433020439:web:c958db1c2c7f9419764a52",
  measurementId: "G-5DY0X8NGTY"
    };
	const app = initializeApp(firebaseConfig);
	const auth = getAuth();
	const user = auth.currentUser;
	export let menu = 0;
	export let uName;
	let uemail='aa';
	/*
	if (user !== null) {
  user.providerData.forEach((profile) => {
    console.log("Sign-in provider: " + profile.providerId);
    console.log("  Provider-specific UID: " + profile.uid);
    console.log("  Name: " + profile.displayName);
    console.log("  Email: " + profile.email);
    console.log("  Photo URL: " + profile.photoURL);
	uemail=profile.email;
  });
}*/
onAuthStateChanged(auth, (user) => {
  if (user) {
    // User is signed in, see docs for a list of available properties
    // https://firebase.google.com/docs/reference/js/firebase.User
    const uid = user.uid;
	uemail = user.email;
    // ...
  } else {
	  uemail='none';
    // User is signed out
    // ...
  }
});
	//let ui = new firebase.AuthUI();

	//const auth = getAuth();
	//const user = auth.currentUser;

	let url = '/';
	//let loggedName="(Unknown)"
	//let loggedName=uName;
/*
	ui.start('#firebaseui-auth-container', {
  signInOptions: [
    // List of OAuth providers supported.
    firebase.auth.GoogleAuthProvider.PROVIDER_ID,
    firebase.auth.FacebookAuthProvider.PROVIDER_ID,
    firebase.auth.TwitterAuthProvider.PROVIDER_ID,
    firebase.auth.GithubAuthProvider.PROVIDER_ID
  ],
  // Other config options...
});*/

</script>
<style>
	.box {
		width: 300px;
		border: 1px solid #aaa;
		border-radius: 2px;
		box-shadow: 2px 2px 8px rgba(0,0,0,0.1);
		padding: 1em;
		margin: 0 0 1em 0;
	}
	h1 {
		
		font-family: 'Comic Sans MS', cursive;
		font-size: 2em;
	}
	ul#menu li{
		display : inline;
	}
	.uname{
		text-align: center;
	}
	.unameDiv{
		border: 1px solid #aaa;
		box-shadow: 2px 2px 8px rgba(0,0,0,0.1);
		padding: 1em;
		margin: 0 0 1em 0;
		width: 200px;
		float:right;
	}
</style>
<h1>File Management</h1>
<div class="unameDiv">
	<p class="uname">Logged info : {uemail}</p>
	</div>
	
<hr>
<ul id="menu">
	<li><a href="/" on:click|preventDefault={() => (navigate("Home", { replace: true }))}>Home</a></li> |
	<li><a href="/" on:click|preventDefault={() => (navigate("Login", { replace: true }))}>Login</a></li> |
	<li><a href="/" on:click|preventDefault={() => (navigate("Logout", { replace: true }))}>Logout</a></li> | 
	<li><a href="/" on:click|preventDefault={() => (navigate("FileUpload", { replace: true }))}>Upload</a></li> | 
	<li><a href="/" on:click|preventDefault={() => (navigate("/", { replace: true }))}>Info</a></li>
</ul>


<!--
{#if menu === 1}
<Login />
{:else if menu === 2}
<Logout />
{:else if menu ===3}
<div class="box">
	<p>● Use firebase to manage your file</p><br>
	<p>xxxxxxxxxx</p>
</div>
{/if}-->

<Router url={url}>
    <div>
        <Route path='/'>
            <Home/>
        </Route>
        <Route path='Logout'>
            <Logout/>
        </Route>
		<Route path='Login'>
			<Login/>
		</Route>
		<Route path='FileUpload'>
			<FileUpload/>
		</Route>
		<Route path='Home'>
			<Home/>
		</Route>
        
    </div>
</Router>
