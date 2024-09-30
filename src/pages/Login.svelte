<script>
    import { getAuth, signInWithPopup, GoogleAuthProvider } from "firebase/auth";
    import { user$ } from "../store";

    const provider = new GoogleAuthProvider();     
    const auth = getAuth();

    const loginWithGoogle =async() =>{
    try{
    const result = await signInWithPopup(auth, provider);
    const credential = GoogleAuthProvider.credentialFromResult(result);
    const token = credential.accessToken;
    const user = result.user;
    user$.set(user);
    localStorage.setItem("token" ,token);
    }catch(error){
    console.error(error);
    }
    };
   
</script>
<div>
    {#if $user$}
    <div>{$user$?.displayName} 로그인됨 </div>
    {/if}
    <div>로그인 하기</div>
    <button class="login-btn" on:click={loginWithGoogle}>
        <img class="google-img" src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTsn_7YWUcHfdiZW2UrAM4XFj_2vk2Opk4mVA&s" 
        alt=""
        />
        <div>Google로 시작하기</div>
    </button>
</div>

<style>
.login-btn{
    width: 200px;
    height: 50px;
    border: 1px solid gray;
    display: flex;
    justify-content: space-between;
    align-items: center;
    cursor: pointer;
    border-radius: 3px;
}
.google-img{
    width: 20px;
}
</style>