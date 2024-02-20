<script lang="ts">
  let response: String;

  let a: number = 0;
  let b: number = 0;

  let newLogin: string = "";
  let newPassword: string = "";

  let login: string = "";
  let password: string = "";

  async function sendRequest() {
    const res = await fetch("/api", {
      method: "GET",
    });

    return res.text();
  }

  async function addNumbers(a: number, b: number) {
    // bierzemy odpowiedź z serwera
    const res = await fetch(`/api/add/${a}/${b}`, {
      method: "GET",
    })

    return res.text();
  }

  async function registerUser() {
    // wywołujemy endpoint z serwera
    const res = await fetch("/api/register", {
      method: "POST",
      // serwer musi wiedzieć, że to, co wysyłamy to JSON
      headers: {
        "Content-Type": "application/json"
      },
      // wysyłamy dane wpisane przez użytkownika
      // JSON.stringify jest po to, by zmienić dane w JSON
      body: JSON.stringify({
        login: newLogin,
        password: newPassword,
      })
    })
  }

  async function loginUser() {
    // wywołujemy endpoint
    const res = await fetch("/api/login", {
      method: "POST",
      // serwer musi wiedzieć, że to, co wysyłamy to JSON
      headers: {
        "Content-Type": "application/json"
      },
      // wysyłamy dane wpisane przez użytkownika
      // JSON.stringify jest po to, by zmienić dane w JSON
      body: JSON.stringify({
        login: login,
        password: password,
      })
    })
  }

  async function getHome() {
    response = await sendRequest();
  }
</script>

<main>
  <div>
    A = <input type="number" bind:value={a} />
    B = <input type="number" bind:value={b} />
    <button on:click={async () => {
      response = await addNumbers(a, b);
    }}>Send request</button>
  
    A + B = {response}
  </div>

  Rejestracja
  <div>
    <!-- Rejestracja -->
    Login: <input bind:value={newLogin} />
    Password: <input bind:value={newPassword} />
    <button on:click={registerUser}>Register</button>
  </div>

  Logowanie
  <div>
    <!-- Logowanie -->
    Login: <input bind:value={login} />
    Password: <input bind:value={password} />
    <button on:click={loginUser}>Login</button>
  </div>
</main>
