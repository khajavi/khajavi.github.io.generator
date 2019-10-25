+++
keywords = [
]
categories = [
]
title = "How to install graalvm ce"
description = ""
date = "2019-10-25T08:59:54+03:30"

+++
```bash
wget https://github.com/oracle/graal/releases/download/vm-19.2.1/graalvm-ce-linux-amd64-19.2.1.tar.gz
tar xvf graalvm-ce-linux-amd64-19.2.1.tar.gz
sudo mv graalvm-ce-19.2.1/ /usr/lib/jvm/
sudo ln -s graalvm-ce-19.2.1/ graalvm
sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/graalvm/bin/java 4
sudo update-alternatives --config java // choose 4
```

add `/usr/lib/jvm/graalvm-ce-19.2.1/bin` to $PATH

install `native-image` by running `gu install native-image`
