FROM golang:1.24.4 AS builder

RUN <<EOT 
  go install github.com/google/go-jsonnet/cmd/jsonnet@latest
  go install github.com/google/go-jsonnet/cmd/jsonnet-lint@latest
  go install github.com/google/go-jsonnet/cmd/jsonnetfmt@latest
  go install github.com/jsonnet-bundler/jsonnet-bundler/cmd/jb@v0.6.0
EOT

FROM mcr.microsoft.com/devcontainers/python:3.14

COPY --from=builder /go/bin/jsonnet /go/bin/jsonnet-lint /go/bin/jsonnetfmt /go/bin/jb /usr/local/bin/

RUN <<EOT
  # Add repo for carapace-bin
  echo "deb [trusted=yes] https://apt.fury.io/rsteube/ /" | tee -a /etc/apt/sources.list.d/carapace.list 
  
  # Install packages and tools
  apt-get update 
  apt-get install -y --no-install-recommends entr git carapace-bin ripgrep

  # setup Alias for kubectl
  echo "alias k=kubectl" | tee -a /home/vscode/.bashrc

  # setup completions
  echo "complete -F __start_kubectl k" | tee -a /home/vscode/.bashrc
  echo "source <(carapace _carapace)" | tee -a /home/vscode/.bashrc
    
  # # setup fzf
  # git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf
  # ~/.fzf/install --all
  # cp ~/.fzf/bin/fzf /usr/local/bin/fzf
  # echo "source <(fzf --bash)" | tee -a /home/vscode/.bashrc
  
  # git clone https://github.com/lincheney/fzf-tab-completion ~/.fzf-completion
  # cp ~/.fzf-completion/bash/fzf-bash-completion.sh /home/vscode/.fzf-bash-completion.sh
  # echo "source ~/.fzf-bash-completion.sh" | tee -a /home/vscode/.bashrc
  # echo "source ~/.fzf-completion/bash/fzf-bash-completion.sh" | tee -a ~/.bashrc
  # echo "bind -x '\"\t\": fzf_bash_completion'" | tee -a ~/.bashrc
  # echo "bind -x '\"\t\": fzf_bash_completion'" | tee -a /home/vscode/.bashrc
EOT

USER vscode

