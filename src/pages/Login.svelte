
<script>
    import { navigate } from "svelte-routing";
    
    
    // 파이어베이스
    import { initializeApp } from "firebase/app";
    import { getAnalytics } from "firebase/analytics";
    import { getAuth, signInWithPopup, GoogleAuthProvider, GithubAuthProvider } from "firebase/auth";
    //import App from "../App.svelte";
    

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
    const analytics = getAnalytics(app);

    const provider = new GoogleAuthProvider();
    const auth = getAuth();
    // 파이어베이스

    
    

    let innerWidth = window.innerWidth;
    let innerHeight = window.innerHeight;
    let userName;
    userName='none';
	
    function clickLoginGithub() {
        
        signInWithPopup(auth, provider).then((result) => {
            const credential = GithubAuthProvider.credentialFromResult(result);
            const token = credential.accessToken;
            const user = result.user;
			const auth = getAuth();
			const userN = auth.currentUser;
            userName=userN;
           
			console.log(userName);
            navigate("Home", { replace: true });
        }).catch((error) => {
            const errorCode = error.code;
            const errorMessage = error.message;
            const email = error.email;
            const credential = GithubAuthProvider.credentialFromError(error);
        });
       
      
    }
    
    
    function clickLoginGoogle() {
        
        signInWithPopup(auth, provider).then((result) => {
            const credential = GoogleAuthProvider.credentialFromResult(result);
            const token = credential.accessToken;
            const user = result.user;
			const auth = getAuth();
			const userN = auth.currentUser;
            userName=userN;

            navigate("Home", { replace: true });
        }).catch((error) => {
            const errorCode = error.code;
            const errorMessage = error.message;
            const email = error.email;
            const credential = GoogleAuthProvider.credentialFromError(error);
        });
        
    
    }

</script>


<svelte:window bind:innerWidth bind:innerHeight/>


<main style="width: {innerWidth}px; height: {innerHeight-250}px">
    <div id="login-section" style="margin-top: {(innerHeight - 600)/2 - 20}px;">
        <div style="margin-left: 70px;">
            <h1>Login with your account</h1>
            
        
        </div>
        <div class="center">
            <button on:click={clickLoginGithub}>
                <!--div id="github-icon"></div-->
                <div>Sign in With GitHub</div>
            </button>
        </div>
        <div class="center">
            <button on:click={clickLoginGoogle}>
                <!--div id="github-icon"></div-->
                <div>Sign in With Google</div>
            </button>
        </div>
        
        <div></div>
    </div>

</main>

<style>
  

    main {
        background-color: #08abf7;
        display: flex;
        justify-content: center;
    }

    #login-section {
        width: 1000px;
        height:400px;
      
        background-color: #ffffff;
        display: flex;
        flex-direction: column;
        justify-content: space-around;
    }

    h1 {
        color: #20154e;
        font-family: 'Georgia', cursive;
        font-weight: 1000;
        font-size: 50px;
        text-align: center;
    }

   

    button {
        width: 200px;
        height: 40px;
        border: 2px solid #C4C4C4;
        border-radius: 10px;
        background-color: #ffffff;
        cursor: pointer;
        display: flex;
        flex-direction: row;
        justify-content: space-evenly;
    }

    button div {
        color: #404040;
        font-size: 14px;
        font-family: 'Noto Sans KR', sans-serif;
        font-weight: 400;
    }
/*
    button #github-icon {
        width: 16px;
        height: 16px;
        margin-top: 3px;
        background-image: url("../icon/githubIcon.png");
    }*/


    .center {
        display: flex;
        justify-content: center;
        flex-direction: row;
    }
</style>