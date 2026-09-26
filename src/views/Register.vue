<template>
<div class="register-page">
  <div>
    <h1>Crea tu cuenta</h1> 
    <p>Completa tus datos para empezar</p>

    </div><br>
    <form @submit.prevent="handleRegister" id="register-container" novalidate>

      <!-- Nombre -->
     <!-- <label>Nombre: </label><br>
        <input id="name"><br>-->

        <div>
          <label for="nombre">Nombre</label>
          <input 
            id="nombre"
            v-model="form.nombre"
            type="text"
            class="form-input"
            :class="{ 'is-invalid': errors.nombre }"
            placeholder="Tu nombre completo"
          />
          <span v-if="errors.nombre" class="error-message">{{ errors.nombre }}</span>
        </div>

        <!--<label>Usuario: </label><br>
        <input id="user"><br>-->

           <!-- Usuario -->
        <div >
          <label for="usuario">Usuario</label>
          <input 
            id="usuario"
            v-model="form.usuario"
            type="text"
            class="form-input"
            :class="{ 'is-invalid': errors.usuario }"
            placeholder="Nombre de usuario"
          />
          <span v-if="errors.usuario" class="error-message">{{ errors.usuario }}</span>
        </div>

        <!--<label>Correo: </label><br>
        <input type="email" id="email"><br>
    <-- Correo Electrónico -->
        <div>
          <label for="correo">Correo electrónico</label>
          <input 
            id="correo"
            v-model="form.correo"
            type="email"
            class="form-input"
            :class="{ 'is-invalid': errors.correo }"
            placeholder="correo@ejemplo.com"
          />
          <span v-if="errors.correo" class="error-message">{{ errors.correo }}</span>
        </div>

      <!--   <label>Contraseña: </label><br>
        <input type=password id="password"><br> -->
<!-- Contraseña -->
        <div class="form-group">
          <label for="password">Contraseña</label>
          <input 
            id="password"
            v-model="form.password"
            type="password"
            class="form-input"
            :class="{ 'is-invalid': errors.password }"
            placeholder="••••••••"
          />
          <span v-if="errors.password" class="error-message">{{ errors.password }}</span>
        </div>

        <!-- Repetir Contraseña -->
        <div class="form-group">
          <label for="confirmPassword">Repetir contraseña</label>
          <input 
            id="confirmPassword"
            v-model="form.confirmPassword"
            type="password"
            class="form-input"
            :class="{ 
              'is-invalid': errors.confirmPassword,
              'is-valid': form.confirmPassword && form.password === form.confirmPassword
            }"
            placeholder="••••••••"
          />
          <span v-if="errors.confirmPassword" class="error-message">{{ errors.confirmPassword }}</span>
        </div>



         <button type="submit" class="btn-submit">
          Registrarse
        </button>


           <!-- Redirección a Login -->
        <div class="login-redirect">
          <span>Si ya tienes una cuenta, </span>
          <router-link to="/login" class="login-link">inicia sesión.</router-link>
        </div>

    </form>



</div>
</template>
<script>
export default {
  name: 'Register',
  data() {
    return {
      form: {
        nombre: '',
        usuario: '',
        correo: '',
        password: '',
        confirmPassword: ''
      },
      errors: {}
    }
  },
  methods: {
    validate() {
      this.errors = {};
      let isValid = true;

      if (!this.form.nombre) {
        this.errors.nombre = 'El nombre es obligatorio.';
        isValid = false;
      }
      if (!this.form.usuario) {
        this.errors.usuario = 'El usuario es obligatorio.';
        isValid = false;
      }
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      if (!this.form.correo || !emailRegex.test(this.form.correo)) {
        this.errors.correo = 'Ingrese un correo electrónico válido.';
        isValid = false;
      }
      if (!this.form.password || this.form.password.length < 6) {
        this.errors.password = 'La contraseña debe tener al menos 6 caracteres.';
        isValid = false;
      }
      if (this.form.password !== this.form.confirmPassword) {
        this.errors.confirmPassword = 'Las contraseñas no coinciden.';
        isValid = false;
      }

      return isValid;
    },
    handleRegister() {
      if (this.validate()) {
        alert('¡Registro enviado con éxito!');
        // Lógica de API o Redirección
      }
    }
  }
}
</script>
<style scoped>
.register-page {
  --primary: #0d9488;
  --primary-dark: #0f766e;
  --text-dark: #17201f;
  --text-medium: #465452;
  --text-light: #687572;
  --background: #f7f9f8;
  --white: #ffffff;
  --card-gray: #f0f3f2;
  --border: #e2e8e6;
  --border-hover: #b9cfcb;
  --gold: #fcd34d;
  
  font-family: 'Poppins', 'Google Sans', sans-serif !important;
  color: var(--text-dark);
  background-color: var(--background);
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 2rem 1.5rem;
}

.register-page * {
  font-family: inherit;
  box-sizing: border-box;
}

h1 {
  color: var(--text-dark);
  font-size: clamp(1.8rem, 4vw, 2.2rem);
  font-weight: 600;
  margin-bottom: 1.5rem;
  text-align: center;
}

#register-container {
  width: 100%;
  max-width: 420px;
  background-color: var(--white);
  border: 1px solid var(--border);
  border-radius: 1rem;
  padding: 2.5rem 2rem;
  box-shadow: 0 10px 25px -5px rgba(15, 118, 110, 0.05);
}

label {
  display: inline-block;
  color: var(--text-medium);
  font-size: 0.82rem;
  font-weight: 600;
  margin-bottom: 0.4rem;
  margin-top: 0.8rem;
}

#register-container label:first-of-type {
  margin-top: 0;
}

input {
  width: 100%;
  padding: 0.8rem 1rem;
  border: 1px solid var(--border);
  border-radius: 0.65rem;
  background-color: var(--background);
  color: var(--text-dark);
  font-size: 0.88rem;
  outline: none;
  transition: border-color 0.2s ease, background-color 0.2s ease;
}

input:focus {
  border-color: var(--primary);
  background-color: var(--white);
}

.btn-submit {
  width: 100%;
  margin-top: 8px;
  background-color: #0d9488;
  color: #ffffff;
  border: none;
  border-radius: 0.65rem;
  padding: 12px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: background-color 0.2s ease, transform 0.1s ease;
}

.btn-submit:hover {
  background-color: #0f766e;
}

.login-redirect {
  text-align: center;
  margin-top: 16px;
  font-size: 0.9rem;
  color: #6b7280;
}

.form-input.is-invalid {
  border-color: #ef4444;
  background-color: #fef2f2;
}

.form-input.is-valid {
  border-color: #10b981;
}

.error-message {
  font-size: 0.78rem;
  color: #ef4444;
}


@media (max-width: 480px) {
  #register-container {
    padding: 1.8rem 1.2rem;
  }
}
</style>