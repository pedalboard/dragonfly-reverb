# Build

build with [elk-audio-os-builder](https://github.com/elk-audio/elk-audio-os-builder)

install sdk

'''
diff --git a/dockerfile b/dockerfile
index 5f682b5..3c0c278 100644
--- a/dockerfile
+++ b/dockerfile
@@ -10,6 +10,7 @@ ARG USERNAME=yoctouser
 ARG GROUPNAME=yocto
 ARG UID=1000
 ARG GID=1000
+ARG SDK_VERSION=1.0.0

 # Set shell
 SHELL ["/bin/bash", "-xo", "pipefail", "-c"]
@@ -108,6 +109,11 @@ RUN git clone https://github.com/siemens/kas.git /opt/kas && \
     git fetch --all --tags && \
     git checkout tags/4.0

+RUN wget https://github.com/elk-audio/elkpi-sdk/releases/download/${SDK_VERSION}/elk-glibc-x86_64-elkpi-audio-os-image-cortexa72-raspberrypi4-64-toolchain-${SDK_VERSION}.sh && \
+    chmod +x elk-glibc-x86_64-elkpi-audio-os-image-cortexa72-raspberrypi4-64-toolchain-${SDK_VERSION}.sh && \
+    ./elk-glibc-x86_64-elkpi-audio-os-image-cortexa72-raspberrypi4-64-toolchain-${SDK_VERSION}.sh -y && \
+    rm elk-glibc-x86_64-elkpi-audio-os-image-cortexa72-raspberrypi4-64-toolchain-${SDK_VERSION}.sh
+
 # Create user without password
 RUN \
  useradd -rm -d /home/$USERNAME -s /bin/bash -g $GROUPNAME -G sudo -u $UID $USERNAME && \
'''

```
docker run --rm  -v ".:/src" -w /src  elk-audio-os-builder sh -c ". /opt/elk/1.0.0/environment-setup-cortexa72-elk-linux && make"
```


