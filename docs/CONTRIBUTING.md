
## Secrets

- Never commit API keys, passwords, access tokens, or other secrets.
- Store local environment variables in `.env`.
- Use `.env.example` to document required environment variables with placeholder values only.
- Ensure `.env` is listed in `.gitignore`.
- Never commit real credentials or share them in issues and pull requests.
- If a secret is exposed, revoke or rotate it immediately and notify the repository maintainers.
