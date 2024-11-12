# Go Development Environment for DMTF Finance and SNIA Swordfish Apps

- [Go Development Environment for DMTF Finance and SNIA Swordfish Apps](#go-development-environment-for-dmtf-finance-and-snia-swordfish-apps)
  - [Building, Testing, and Deploying the Container Image](#building-testing-and-deploying-the-container-image)
    - [Building in Interactive Mode](#building-in-interactive-mode)
      - [On a Linux Host](#on-a-linux-host)
      - [On a Windows Host](#on-a-windows-host)
      - [In the Linux Guest](#in-the-linux-guest)
    - [Building in Batch Mode](#building-in-batch-mode)
      - [On a Linux Host](#on-a-linux-host-1)
      - [On a Windows Host](#on-a-windows-host-1)

## Building, Testing, and Deploying the Container Image

```powershell
cd /Path/To/Development-Environments
```

### Building in Interactive Mode

#### On a Linux Host

```bash
docker run \
    --interactive \
    --tty \
    --name development-environments-go-for-finance \
    --volume '/Path/To/Development-Environments:/src' \
    --workdir /build \
    docker.io/ubuntu:24.10
```

```bash
docker start --interactive development-environments-go-for-finance
```

#### On a Windows Host

```powershell
docker run `
    --interactive `
    --tty `
    --name development-environments-go-for-finance `
    --volume '/Path/To/Development-Environments:/src' `
    --workdir /build `
    docker.io/ubuntu:24.10
```

```powershell
docker start --interactive development-environments-go-for-finance
```

#### In the Linux Guest

```bash
apt-get update

apt-get install --yes --no-install-recommends \
    ca-certificates \
    curl

rm -rf /usr/local/go

curl -fsSL https://go.dev/dl/go1.23.3.linux-amd64.tar.gz | tar -xzf - -C /usr/local

apt-get remove --yes --purge \
    curl

apt-get autoremove --yes --purge

rm -rf /var/lib/apt/lists/*
```

```bash
export PATH=/usr/local/go/bin${PATH:+:${PATH}}
```

```bash
cd /build
```

```bash
go mod init skeleton
go get github.com/spf13/cobra@v1.8.1
go get github.com/spf13/viper@v1.19.0
go get github.com/go-logr/logr@v1.4.2
go get github.com/go-logr/zerologr@v1.2.3
go get github.com/stmcginnis/gofish@v0.20.0
go mod vendor
```

### Building in Batch Mode

#### On a Linux Host

```bash
docker build \
    --file DevOps/Docker/Go-For-Finance/SDK/Dockerfile \
    --tag docker.io/eajkseajks/go-for-finance-sdk:0.0.0 \
    .
```

#### On a Windows Host

```powershell
docker build `
    --file DevOps/Docker/Go-For-Finance/SDK/Dockerfile `
    --tag docker.io/eajkseajks/go-for-finance-sdk:0.0.0 `
    .
```
