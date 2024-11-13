<script setup lang="ts">
const supabase = useSupabaseClient()
const email = ref('')

const signInWithOtp = async () => {
  console.log("Button clicked"); // This will confirm the function is being called
  const { error } = await supabase.auth.signInWithOtp({
    email: email.value,
    options: {
      emailRedirectTo: 'http://localhost:3000/confirm',
    }
  });
  if (error) {
    console.error("Error signing in with OTP:", error);
  } else {
    console.log("OTP sent successfully!");
  }
}
</script>

<template>
  <div class="login-container">
    <input
      v-model="email"
      type="email"
      placeholder="Enter your email"
      class="input-field"
    />
    <button @click="signInWithOtp" class="login-button">
      Sign In with E-Mail
    </button>
  </div>
</template>

<style scoped>
.login-container {
  max-width: 400px;
  padding: 2rem;
  border: 1px solid #ccc;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);

  /* Centering on the screen */
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  flex-direction: column;
  align-items: center;
}

.input-field {
  width: 100%;
  padding: 0.75rem;
  margin-bottom: 1rem;
  font-size: 1rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  outline: none;
  box-sizing: border-box;
}

.login-button {
  width: 100%;
  padding: 0.75rem;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
  transition: background-color 0.3s ease;
}

.login-button:hover {
  background-color: #0056b3;
}
</style>
