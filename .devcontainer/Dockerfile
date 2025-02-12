FROM golang:1.24.0 AS builder

RUN go install github.com/google/go-jsonnet/cmd/jsonnet@latest && \
  go install github.com/google/go-jsonnet/cmd/jsonnet-lint@latest && \
  go install github.com/google/go-jsonnet/cmd/jsonnetfmt@latest && \
  go install github.com/jsonnet-bundler/jsonnet-bundler/cmd/jb@v0.6.0

FROM mcr.microsoft.com/devcontainers/python:3.13

COPY --from=builder /go/bin/jsonnet /go/bin/jsonnet-lint /go/bin/jsonnetfmt /go/bin/jb /usr/local/bin/

RUN sudo apt update && sudo apt install -y --no-install-recommends \
  entr git &&\
  echo "alias k=kubectl" >> /home/vscode/.bashrc &&\
  echo "complete -F __start_kubectl k" >> /home/vscode/.bashrc
