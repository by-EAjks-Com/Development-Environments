# Go Development Environment for Kubernetes Apps

- [Go Development Environment for Kubernetes Apps](#go-development-environment-for-kubernetes-apps)
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
    --name development-environments-go-for-kubernetes \
    --volume '/Path/To/Development-Environments:/src' \
    --workdir /build \
    docker.io/ubuntu:24.10
```

```bash
docker start --interactive development-environments-go-for-kubernetes
```

#### On a Windows Host

```powershell
docker run `
    --interactive `
    --tty `
    --name development-environments-go-for-kubernetes `
    --volume '/Path/To/Development-Environments:/src' `
    --workdir /build `
    docker.io/ubuntu:24.10
```

```powershell
docker start --interactive development-environments-go-for-kubernetes
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
go get k8s.io/client-go@v0.31.2
go get go.opentelemetry.io/otel@v1.32.0
go get go.opentelemetry.io/otel/sdk@v1.32.0
go get go.opentelemetry.io/otel/sdk/log@v0.8.0
go get go.opentelemetry.io/otel/sdk/metric@v1.32.0
go get go.opentelemetry.io/otel/sdk/trace@v1.32.0
go get go.opentelemetry.io/otel/exporters/stdout/stdoutlog@v0.8.0
go get go.opentelemetry.io/otel/exporters/stdout/stdoutmetric@v1.32.0
go get go.opentelemetry.io/otel/exporters/stdout/stdouttrace@v1.32.0
go get github.com/prometheus/client_golang@v1.20.5
go get github.com/elastic/go-elasticsearch/v8@v8.14.0
go mod vendor
```

### Building in Batch Mode

#### On a Linux Host

```bash
docker build \
    --file DevOps/Docker/Go-For-Kubernetes/SDK/Dockerfile \
    --tag docker.io/eajkseajks/go-for-kubernetes-sdk:0.0.0 \
    .
```

#### On a Windows Host

```powershell
docker build `
    --file DevOps/Docker/Go-For-Kubernetes/SDK/Dockerfile `
    --tag docker.io/eajkseajks/go-for-kubernetes-sdk:0.0.0 `
    .
```
