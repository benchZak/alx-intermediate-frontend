#using docker
1. 🗂 Create a working directory
```bash
mkdir sass-ubuntu
cd sass-ubuntu
```

2. 📝 Create a Dockerfile
```bash
# Dockerfile
FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive

# Install dependencies
RUN apt-get update && apt-get install -y curl git bash nano

# Install nvm (Node Version Manager)
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

# Add nvm to environment
ENV NVM_DIR /root/.nvm
RUN bash -c "source $NVM_DIR/nvm.sh && \
             nvm install 20.16.0 && \
             nvm use 20.16.0 && \
             npm install -g sass@3.7.4 && \
             echo 'Step 1: curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash' >> /root/0-installation-script && \
             echo 'Step 2: exit and reopen the terminal' >> /root/0-installation-script && \
             echo 'Step 3: nvm install 20.16.0' >> /root/0-installation-script && \
             echo 'Step 4: npm install sass -v 3.7.4' >> /root/0-installation-script"

CMD ["/bin/bash"]

```

```bash
docker build -t sass-ubuntu .
docker run -it --name sass-container sass-ubuntu
```
```bash
sass --version
```
You should see:
```bash
1.32.0 compiled with dart2js 2.x.x
```
