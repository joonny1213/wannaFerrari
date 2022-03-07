<script>
 import { navigate } from "svelte-routing";
 import { getAuth, signOut } from "firebase/auth";
 import { onMount } from 'svelte';
import { FirebaseError } from "firebase/app";
 const auth = getAuth();
 
 //function clickLogout(){
     onMount(async()=> {
        signOut(auth).then(() => {
  // Sign-out successful.
  alert("Sign-out successful");
  navigate("Home", { replace: true });
}).catch((error) => {
  // An error happened.
});
     })

     /*
signOut(auth).then(() => {
  // Sign-out successful.
  alert("Sign-out successful");
 // navigate("LogoutMessage", { replace: true });
}).catch((error) => {
  // An error happened.
});*/
// }
/*
firebase.auth().signOut().then(() =>{
    navigate
})*/
    //navigate("home", { replace: true });
</script>
<!--
<div class="center">
    <button on:click={clickLogout}>
        <div>Logout</div>
    </button>
</div>  -->

