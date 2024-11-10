# Go Development Environment

- [Go Development Environment](#go-development-environment)
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
cd /Path/To/Development-Environment-Go
```

### Building in Interactive Mode

#### On a Linux Host

```bash
docker run \
    --interactive \
    --tty \
    --name development-environment-go \
    --volume '/Path/To/Development-Environment-Go:/src' \
    --workdir /build \
    docker.io/ubuntu:24.04
```

```bash
docker start --interactive development-environment-go
```

#### On a Windows Host

```powershell
docker run `
    --interactive `
    --tty `
    --name development-environment-go `
    --volume '/Path/To/Development-Environment-Go:/src' `
    --workdir /build `
    docker.io/ubuntu:24.04
```

```powershell
docker start --interactive development-environment-go
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
mkdir /build && cd /build
```

```bash
go mod init skeleton
go get github.com/spf13/cobra@latest
go get github.com/spf13/viper@latest
go get github.com/go-kit/log@latest
go get github.com/go-logr/logr@latest
go get github.com/rs/zerolog@latest
go get github.com/sirupsen/logrus@latest
go get golang.org/x/net@latest
go get golang.org/x/sys@latest
go get github.com/valyala/fasthttp@latest
go get github.com/gofiber/fiber/v3@latest
go get github.com/gin-gonic/gin@latest
go get github.com/gorilla/csrf@latest
go get github.com/gorilla/handlers@latest
go get github.com/gorilla/mux@latest
go get github.com/gorilla/pat@latest
go get github.com/gorilla/reverse@latest
go get github.com/gorilla/rpc@latest
go get github.com/gorilla/schema@latest
go get github.com/gorilla/securecookie@latest
go get github.com/gorilla/sessions@latest
go get github.com/gorilla/websocket@latest
go get golang.org/x/oauth2@latest
go get github.com/coreos/go-oidc/v3/oidc@latest
go get github.com/go-kit/kit@latest
go get gorm.io/gorm@latest
go get gorm.io/driver/sqlite@latest
go get gorm.io/driver/mysql@latest
go get gorm.io/driver/sqlserver@latest
go get gorm.io/driver/postgres@latest
go get github.com/pressly/goose@latest
go get github.com/smartystreets/goconvey@latest
go get github.com/stmcginnis/gofish@latest
go get k8s.io/client-go@latest
go get github.com/elastic/go-elasticsearch/v8@latest
go get github.com/aws/aws-sdk-go-v2@latest
go get github.com/ovh/go-ovh@latest
go mod vendor
```

### Building in Batch Mode

#### On a Linux Host

```bash
docker build \
    --file DevOps/Docker/Ubuntu-24.04/SDK/Dockerfile \
    --tag docker.io/eajkseajks/development-environment-co:0.0.0-sdk-ubuntu-24.04 \
    .
```

#### On a Windows Host

```powershell
docker build `
    --file DevOps/Docker/Ubuntu-24.04/SDK/Dockerfile `
    --tag docker.io/eajkseajks/development-environment-co:0.0.0-sdk-ubuntu-24.04 `
    .
```
