<template>
  <div class="login">
    <section class="bg-login">
      <div class="credentials-content">
        <h1>Kd Meu Pet</h1>
        <p>Seu bichinho a um clique de você.</p>
      </div>
    </section>

    <section class="bg-form">
      <div class="bg-formContent">
        <h1>Login</h1> <br />

      <form @submit.prevent="makeLogin">
        <label for="email">E-mail:</label>
        <input
					type="email"
					v-model="user.email"
          class="form-control"
          required>
        <br><br>

        <label for="password">Senha:</label>
        <input type="password"
              minlength="6"
              maxlength="24"
							v-model="user.password"
            	class="form-control"
              required> <br><br>

        <div class="center-content">
          <button class="botao-padrao" id="js-submitItem">Fazer login</button> <br />
        </div>

      </form>
      <div class="footer-register"> Não possui conta, ainda?!
          <a href="/cadastro"> Criar conta</a>
      </div>

      </div>
    </section>
  </div>
</template>

<script>
export default {
	name: 'Login',
	data() {
		return {
			user: {}
		};
	},
	methods: {
		makeLogin() {
			const url = "auth/usuario/login";
			this.$http.post(url, this.user)
			.then(response => {
        console.log(response.data);
				this.$store.state.token = response.data.token;
				this.$store.state.user = response.data.user;
				this.$router.push({ name: 'UserPage'});
			}).catch(error => {
				console.log(error);
			});
		},
	},
};
</script>

<style scoped>

input[data-v-2529d779] {
    background: transparent;
    border: 0;
    border-bottom: 1px solid #dadad9;
    width: 400px;
    height: 30px;
    font-size: 1.4em;
}

.login {
  display: flex;
}

.bg-login {
	background: url('../../assets/login-cover.jpeg') center;
	background-repeat: no-repeat;
	background-size: cover;
	width: 50vw;
	height: 100vh;
	display: flex;
	flex-direction: column-reverse;
	flex-wrap: wrap;
  justify-content: center;
  align-items: center;
}

.credentials-content {
	padding: 10px;
}

.credentials-content h1 {
	color: #fff;
	font-size: 5em;
	text-shadow: 2px 1px #222;
}

.credentials-content p {
	color: #fff;
	letter-spacing: 4px;
	font-size: 1.4em;
	text-shadow: 1px 1px #222;
	padding-left: 20px;
	padding-bottom: 0;
}


.bg-form {
	width: 50vw;
	height: 100vh;
	border-top: 1px solid #eee;
	padding: 20px;
	display: flex;
	justify-content: center;
	align-items: center;
	flex-wrap: wrap;
}

.bg-formContent {
	width: 400px;
	display: flex;
	flex-wrap: wrap;
	justify-content: center;
}

h1 {
	color: #222;
	font-size: 2em;
	text-align: center;
}

p {
	padding: 20px 0;
	text-align: center;
}

.botao-padrao {
	margin-top: 20px;
	width: 160px;
	color: #fff;
	padding: 10px;
	border: transparent;
	font-size: 1em;
	cursor: pointer;
}

.botao-padrao:hover {
  margin-top: 20px;
  width: 160px;
  background: #E63946;
  color: #fff;
  padding: 10px;
  border: transparent;
  font-size: 1em;
  cursor: pointer;
}

label {
	color: #95a5a6;
	font-size: .8em;
	font-weight: bold;
}

.required::after {
	content: '*';
	padding-left: 5px;
	color: #e74c3c;
	font-size: 1.3em
}

input {
	background: transparent;
	border: 0;
	border-bottom: 1px solid #3498db;
	width: 400px;
	height: 30px;
	font-size: 1.4em;
}

input:focus {
  outline: none;
	border-bottom: 2px solid #34495e;
}

.center-content {
	display: flex;
	flex-wrap: wrap;
	justify-content: center;
}

.form-valid--error {
	font-size: .9em;
	color: red;
}

.form-valid--error p {
	text-align: left;
	font-size: .9em;
	color: red;
}

.footer-register a {
  color: #4ecdc4;
}

.footer-register {
  padding-top: 40px;
}
</style>
