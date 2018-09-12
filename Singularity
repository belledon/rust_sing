bootstrap: docker
from: ubuntu:latest

%runscript
 if [ ! -d "$RROOT" ]; then
     echo "No rust libs found at $RROOT"
     cp -r "/rust" "$RROOT"
     echo "Exported base installation to $RROOT"
 fi
 exec "$@"

%environment
  ROOT="$( git rev-parse --show-toplevel )"
  export RROOT="$ROOT/.rust"
  export CARGO_HOME="$RROOT/cargo"
  export RUSTUP_HOME="$RROOT/rustup"
  export PATH=$PATH:/$CARGO_HOME/bin

%post
  apt-get update
  apt-get install -y curl gcc git wget
  mkdir /rust
  mkdir /rust/cargo
  mkdir /rust/rustup
  export CARGO_HOME="/rust/cargo"
  export RUSTUP_HOME="/rust/rustup"
  cd /rust
  curl https://sh.rustup.rs -sSf > install.sh
  sh install.sh -y
