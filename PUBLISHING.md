# Publishing checklist

1. Replace `YOUR_GITHUB_USERNAME` in `README.md` and `plugins/principal-frontend-engineer/.claude-plugin/plugin.json`.
2. Push this repository to GitHub as `principal-frontend-engineer`.
3. Validate locally:

```bash
claude plugin validate .
claude plugin validate ./plugins/principal-frontend-engineer
```

4. Test marketplace install locally:

```bash
claude plugin marketplace add ./principal-frontend-engineer
claude plugin install principal-frontend-engineer@principal-frontend-engineer
```

5. Test from GitHub:

```bash
claude plugin marketplace add YOUR_GITHUB_USERNAME/principal-frontend-engineer
claude plugin install principal-frontend-engineer@principal-frontend-engineer
```
