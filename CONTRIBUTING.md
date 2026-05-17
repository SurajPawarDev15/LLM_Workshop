# Contributing

Thanks for wanting to contribute! Keep contributions small and focused.

Suggested workflow

1. Fork the repository and create a feature branch: `git checkout -b feat/your-feature`
2. Implement your change and include tests where appropriate.
3. Run the backend and frontend locally to verify behavior:

```bash
# backend
cd backend
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
python main.py

# frontend
cd frontend
npm install
npm run dev
```

4. Commit with clear messages and open a Pull Request with a description of the change and any migration notes.

Code style

- Keep changes well-documented and include inline comments for non-obvious logic.
- Add unit tests where practical.

Communication

- Use the PR description to explain intent, scope, and any backward-incompatible changes.

License

By contributing you agree that your contributions will be licensed under the project's license.
