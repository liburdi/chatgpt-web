GOPATH:=$(shell go env GOPATH)
GoVersion=$(shell go version)
BuildTime=$(shell date +%F-%Z/%T)
CommitID=$(shell git rev-parse HEAD)

LDFLAGS=-ldflags "-X 'gitlab.weipaitang.com/tech-lab/dionysus.GoVersion=${GoVersion}' \
-X gitlab.weipaitang.com/tech-lab/dionysus.BuildTime=${BuildTime} \
-X gitlab.weipaitang.com/tech-lab/dionysus.CommitID=${CommitID}"  \


build:
	go mod tidy
	go build ${LDFLAGS} -v -o bin/chatgpt-go cmd/main.go

run.api:
	 go run cmd/main.go