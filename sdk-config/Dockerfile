# Dockerfile-tools. Use the official Ubuntu image.
FROM ubuntu:jammy-20240427

# Set label metadata
LABEL description="Base Ubuntu image with Java and Android SDK installed"
LABEL org.opencontainers.image.source=https://github.com/theHprogrammer/dockernize-the-flutter

USER root

# Set environment variables
ENV ANDROID_HOME=/opt/android-sdk
ENV JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64
ENV PATH="$JAVA_HOME/bin:$ANDROID_HOME/cmdline-tools/latest/bin:$ANDROID_HOME/platform-tools:$ANDROID_HOME/emulator:$PATH"

# Set environment variables for build tools and NDK
ENV ANDROID_PLATFORM_VERSION 34
ENV ANDROID_BUILD_TOOLS_VERSION 34.0.0
# ENV ANDROID_NDK_VERSION 26.2.11394342

# Install necessary packages
RUN apt-get update -y && apt-get upgrade -y \
    && apt-get install -y curl git unzip xz-utils zip libglu1-mesa \
    && apt-get install -y jq \
    && apt-get install -y openjdk-21-jdk \
    && apt-get install -y apt-utils locales wget software-properties-common build-essential automake autoconf libreadline-dev libncurses-dev libssl-dev libyaml-dev libxslt-dev libffi-dev libtool unixodbc-dev libsqlite3-dev sqlite3 openssh-client --no-install-recommends \
    && apt-get install -y clang cmake ninja-build pkg-config libgtk-3-dev \
    && dpkg --add-architecture i386 \
    && apt-get update -y \
    # Install develop and build tools with multiarch support
    && apt-get install -y libc6:i386 libncurses5:i386 libstdc++6:i386 lib32z1 libbz2-1.0:i386 \
    # Clean up
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    # Download and install Android Command Line Tools
    && mkdir -p $ANDROID_HOME/cmdline-tools \
    && wget -O cmdline-tools.zip "https://dl.google.com/android/repository/commandlinetools-linux-11076708_latest.zip" \
    && unzip cmdline-tools.zip -d $ANDROID_HOME/cmdline-tools \
    && mv $ANDROID_HOME/cmdline-tools/cmdline-tools $ANDROID_HOME/cmdline-tools/latest \
    && rm cmdline-tools.zip \
    && sdkmanager --update \
    # Accept licenses
    && yes | sdkmanager --licenses \
    # Install SDK Platforms and Platform Tools
    && yes | sdkmanager \ 
    "platforms;android-$ANDROID_PLATFORM_VERSION" \
    "build-tools;$ANDROID_BUILD_TOOLS_VERSION" \
    # "ndk;$ANDROID_NDK_VERSION" \
    "platform-tools"

WORKDIR /home
