# CLI

← [Назад][back]

---

## Commands

### New

Create an env vault for your project.
Keep your secrets safe init. [Read more](https://www.dotenv.org/docs/dotenv-vault/new)

```shell
npx dotenv-vault@latest new
```

### Push

Push your `.env` file securely. [Read more](https://www.dotenv.org/docs/dotenv-vault/push)

```shell
npx dotenv-vault@latest push
```

### Pull

Pull your `.env` file securely. [Read more](https://www.dotenv.org/docs/dotenv-vault/pull)

```shell
npx dotenv-vault@latest pull
```

### Build

Build your localized encrypted `.env.vault` file for use with
deploy. [Read more](https://www.dotenv.org/docs/dotenv-vault/build)

```shell
npx dotenv-vault@latest build
```

### Keys

List your `.env.vault` decryption keys for use with deploy. [Read more](https://www.dotenv.org/docs/dotenv-vault/keys)

```shell
# List all your keys.
npx dotenv-vault@latest keys

# List a single environment key.
npx dotenv-vault@latest keys production
```

### Open

Open the UI to your env vault. Manage multiple environments. [Read more](https://www.dotenv.org/docs/dotenv-vault/open)

```shell
npx dotenv-vault@latest open
```

### Login

Log in to `dotenv-vault`. [Read more](https://www.dotenv.org/docs/dotenv-vault/login)

```shell
npx dotenv-vault@latest login
```

### Logout

Log out of `dotenv-vault`. [Read more](https://www.dotenv.org/docs/dotenv-vault/logout)

```shell
npx dotenv-vault@latest logout
```

### Whoami

Display the current logged-in user. [Read more](https://www.dotenv.org/docs/dotenv-vault/whoami)

```shell
npx dotenv-vault@latest whoami
```

### Versions

List version history for your env vault. [Read more](https://www.dotenv.org/docs/dotenv-vault/versions)

```shell
npx dotenv-vault@latest version
```

### Rotatekey

Rotate a project environment's `DOTENV_KEY`. [Read more](https://www.dotenv.org/docs/dotenv-vault/rotatekey)

```shell
npx dotenv-vault@latest rotatekey
```

### Status

Check `dotenv-vault` operational status. [Read more](https://www.dotenv.org/docs/dotenv-vault/status)

```shell
npx dotenv-vault@latest status
```

### Help

Display help for `dotenv-vault`. [Read more](https://www.dotenv.org/docs/dotenv-vault/help)

```shell
npx dotenv-vault@latest help

# npx dotenv-vault@latest help [COMMAND]
npx dotenv-vault@latest help keys
```

---

← [Назад][back]

[back]: <.> "Назад к оглавлению"
