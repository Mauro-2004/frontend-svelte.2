<script>
  import { onMount } from "svelte";

  let email = "";
  let password = "";
  let errorMessage = "";

  function handleSubmit() {
    errorMessage = "";

    if (!email || !password) {
      errorMessage = "Todos los campos son obligatorios";
      return;
    }

    // Simulación de autenticación
    if (email === "admin@example.com" && password === "123456") {
      alert("Inicio de sesión exitoso ✅");
    } else {
      errorMessage = "Correo o contraseña incorrectos ❌";
    }
  }
</script>

<div class="login-container">
  <h2>Iniciar Sesión</h2>
  {#if errorMessage}
    <p class="error">{errorMessage}</p>
  {/if}
  <form on:submit|preventDefault={handleSubmit}>
    <label for="email">Correo electrónico</label>
    <input type="email" id="email" bind:value={email} placeholder="Ingresa tu correo" required />

    <label for="password">Contraseña</label>
    <input type="password" id="password" bind:value={password} placeholder="Ingresa tu contraseña" required />

    <button type="submit">Iniciar Sesión</button>
  </form>
</div>

<style>
  .login-container {
    max-width: 320px;
    margin: auto;
    padding: 20px;
    background: #fff;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
    text-align: center;
  }

  h2 {
    color: #333;
  }

  .error {
    color: red;
    font-size: 14px;
  }

  form {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }

  label {
    font-weight: bold;
    text-align: left;
  }

  input {
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    font-size: 16px;
  }

  button {
    background: #007bff;
    color: white;
    border: none;
    padding: 10px;
    cursor: pointer;
    border-radius: 5px;
    font-size: 16px;
  }

  button:hover {
    background: #0056b3;
  }
</style>
