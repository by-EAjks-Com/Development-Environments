# Minimal Go Development Environment

- [Minimal Go Development Environment](#minimal-go-development-environment)
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
    --name development-environments-go-minimal \
    --volume '/Path/To/Development-Environments:/src' \
    --workdir /build \
    docker.io/ubuntu:24.10
```

```bash
docker start --interactive development-environments-go-minimal
```

#### On a Windows Host

```powershell
docker run `
    --interactive `
    --tty `
    --name development-environments-go-minimal `
    --volume '/Path/To/Development-Environments:/src' `
    --workdir /build `
    docker.io/ubuntu:24.10
```

```powershell
docker start --interactive development-environments-go-minimal
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

### Building in Batch Mode

#### On a Linux Host

```bash
docker build \
    --file DevOps/Docker/Go-Minimal/SDK/Dockerfile \
    --tag docker.io/eajkseajks/go-minimal-sdk:0.0.0 \
    .
```

#### On a Windows Host

```powershell
docker build `
    --file DevOps/Docker/Go-Minimal/SDK/Dockerfile `
    --tag docker.io/eajkseajks/go-minimal-sdk:0.0.0 `
    .
```
