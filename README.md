## Local Github Action Testing with `act`

Run GitHub Actions (`act`) locally both for root and non root user.

### Prerequisites

Ensure `curl`, `sudo` and `docker` are installed on your host system, and `docker` is running and allowed to run by curret user.


### Installation

```bash
curl https://raw.githubusercontent.com/nektos/act/master/install.sh | sudo bash
```

### File: `.github/workflows/tests.yml`
k is current username in line  `cp /home/k/github-action . -r   `

github-action is current project dir

```yaml
name: Tests
on:
  push:
    branches: [ main ]
jobs:
  build:
    runs-on: ubuntu-24.04
    container:
      image: ubuntu:24.04
    steps:
      - uses: actions/checkout@v4
      - name: root
        run: |
          whoami
          pwd
          ls -lah
      - uses: actions/checkout@v4
      - name: non root
        shell: su - ubuntu -c "bash {0}"
        run: |
          cp /home/k/github-action . -r && cd github-action
          whoami
          pwd
          ls -lah
```

### Execution Command

Navigate to the project root directory and run:

```bash
act push
```
