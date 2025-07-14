curl -s "https://get.sdkman.io" | bash

source "$HOME/.sdkman/bin/sdkman-init.sh"

sdk list java

sdk install java 8.0.442-temurin

sdk default java 8.0.442-temurin