## Local Github Action Testing with `act`

Run GitHub Actions (`act`) locally both for root and non root user.

### Prerequisites

Ensure `curl`, `sudo` and `docker` are installed on your host system, and `docker` is running and allowed to run by current user.

### Installation

```bash
curl https://raw.githubusercontent.com/nektos/act/master/install.sh | sudo bash
```

### File: `.github/workflows/test.yml`
k is current username in line `cp /home/k/github-action-local . -r`

github-action-local is current project dir

```yaml
name: Tests
on:
  push:
    branches: [ main ]
jobs:
  build:
    runs-on: ubuntu:local
    steps:
      - uses: actions/checkout@v4
      - name: default user
        run: |
          whoami
          pwd
      - name: user runner
        shell: su - runner -c "bash {0}"
        run: |
          cp /home/k/github-action-local . -r && cd github-action-local
          whoami
          curl -V
```

### Execution Command

Navigate to the project root directory and run:

```bash
act push -P ubuntu-latest=ubuntu:local --pull=false
```

or

```bash
alias act="act -P ubuntu-latest=ubuntu:local --pull=false"
act push
```
