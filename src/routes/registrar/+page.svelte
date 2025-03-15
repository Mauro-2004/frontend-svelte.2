<script>
  import { onMount } from "svelte";

  let nombre = "";
  let email = "";
  let password = "";
  let confirmPassword = "";
  let error = "";
  let success = false;

  function validarFormulario() {
    error = "";

    if (!nombre || !email || !password || !confirmPassword) {
      error = "Todos los campos son obligatorios.";
      return false;
    }

    if (!email.includes("@")) {
      error = "Correo inválido.";
      return false;
    }

    if (password.length < 6) {
      error = "La contraseña debe tener al menos 6 caracteres.";
      return false;
    }

    if (password !== confirmPassword) {
      error = "Las contraseñas no coinciden.";
      return false;
    }

    return true;
  }

6
    function sendEmail() {
        emailjs.init(apikey); 
        emailjs.send(serviceID, templateID, {
            nombre: v_nombre,
            email: v_usuario, 
        })
        .then(result => {
            alert('Correo enviado con éxito!');
        })
        .catch(error => {
            console.log('Error al enviar el correo:', error.text);
        });
    }

    let v_password = "";
    let passwordInsegura = "";
    let v_same_password = "";
    let r_pass = "";
    let v_nombre = "";
    let v_apellido = "";
    let v_documento = "";
    let v_telefono = "";
    let v_email = "";
    let v_rol = "";
    let v_id_producto = "";
    let v_estado = "";

    async function Register(event) {
        try {
            event.preventDefault(); // Evita que el formulario se envíe automáticamente
        
           
      
            if (v_password==r_pass){
                    v_same_password=false
            }else{
                v_same_password=true
                passwordInsegura=false
                return;
            }

            await checkPasswordSecurity(); // Verificar seguridad de la contraseña
             
        
            if (passwordInsegura) {
                alert("⚠️ El nivel de seguridad de la contraseña es debil, no olvides incluir mayuscula y caracter especiales");
                return;
            }else{
                passwordInsegura=false

            }

        
                const response = await fetch("https://backend-fastapi-gvnr.onrender.com/create_user", {
                    method: "POST",
                    headers: {
                        "Content-Type": "application/json",
                    },
                    body: JSON.stringify({
                        nombre: v_nombre,
                        apellido: v_apellido,
                        documento: v_documento,
                        telefono: v_telefono,
                        email: v_email,
                        password: v_password,
                        id_rol: v_rol,
                        id_producto: v_id_producto,
                        estado: v_estado
                    }),
                });

                const data = await response.json();
                console.log(data);
            

                if (data!="Informacion") {
                    Swal.fire({
                        title: "Registrado!",
                        text: "Usuario ha sido registrado",
                        icon: "success",
                    });
                    setTimeout(() => {
                    location.reload();
                    }, 3000);
                
                    //sendEmail()
                } else {
                    alert("Usuario ya registrado");
                }
            } catch (e) {
                error = e.message;
                alert("Error en la solicitud: " + error);
            }
    }



    async function sha1(str) {
        const buffer = new TextEncoder().encode(str);
        const hashBuffer = await crypto.subtle.digest('SHA-1', buffer);
        const hashArray = Array.from(new Uint8Array(hashBuffer));
        return hashArray.map(b => b.toString(16).padStart(2, '0')).join('').toUpperCase();
    }


    async function checkPasswordSecurity() {
        if (!v_password) return;
        
        const hash = await sha1(v_password);
        const prefix = hash.substring(0, 5);
        const suffix = hash.substring(5).toUpperCase();

        try {
            const response = await fetch(`https://api.pwnedpasswords.com/range/${prefix}`);
            const data = await response.text();
            
            passwordInsegura = data.split("\n").some(line => line.split(":")[0] === suffix);
        } catch (error) {
            console.error("Error verificando la contraseña:", error);
        }
    }
  
</script>

<div class="registro-container">
  <h1>📝 Registro</h1>

  {#if error}
    <p class="error">{error}</p>
  {/if}

  {#if success}
    <p class="success">✅ ¡Registro exitoso! 🎉</p>
  {/if}

  <form on:submit|preventDefault={Register}>
    <label>Nombre Completo</label>
    <input type="text" bind:value={nombre} placeholder="Tu nombre" />

    <label>Correo Electrónico</label>
    <input type="email" bind:value={email} placeholder="ejemplo@correo.com" />

    <label>Contraseña</label>
    <input type="password" bind:value={password} placeholder="Mínimo 6 caracteres" />

    <label>Confirmar Contraseña</label>
    <input type="password" bind:value={confirmPassword} placeholder="Repite tu contraseña" />

    <button type="submit">Registrarse</button>
  </form>
</div>

<style>
  .registro-container {
    max-width: 400px;
    margin: auto;
    padding: 20px;
    background: #f9f9f9;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  }

  h1 {
    text-align: center;
    color: #333;
  }

  form {
    display: flex;
    flex-direction: column;
  }

  label {
    margin-top: 10px;
    font-weight: bold;
    color: #555;
  }

  input {
    padding: 10px;
    margin-top: 5px;
    border: 1px solid #ccc;
    border-radius: 5px;
  }

  button {
    margin-top: 15px;
    padding: 10px;
    background: #28a745;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
  }

  button:hover {
    background: #218838;
  }

  .error {
    color: red;
    font-weight: bold;
    text-align: center;
  }

  .success {
    color: green;
    font-weight: bold;
    text-align: center;
  }
</style>
