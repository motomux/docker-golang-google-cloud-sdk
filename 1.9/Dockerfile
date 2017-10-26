FROM golang:1.9.2

MAINTAINER motomux <motomux@gmail.com>

ENV PATH="/opt/google-cloud-sdk/bin:${PATH}"

# Install python
RUN apt-get update \
 && apt-get install -y --no-install-recommends python

# install gcloud and kubernetes
RUN mkdir /opt/google-cloud-sdk \
 && curl -L https://dl.google.com/dl/cloudsdk/channels/rapid/google-cloud-sdk.tar.gz | tar xvz -C /opt \
 && CLOUDSDK_CORE_DISABLE_PROMPTS=1 /opt/google-cloud-sdk/install.sh \
 && gcloud config set disable_usage_reporting true \
 && CLOUDSDK_CORE_DISABLE_PROMPTS=1 gcloud components install kubectl

# Install Docker
RUN apt-get update \
 && apt-get install -y apt-transport-https ca-certificates curl gnupg2 software-properties-common \
 && curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg | apt-key add - \
 && apt-key fingerprint 0EBFCD88 \
 && add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") $(lsb_release -cs) stable" \
 && apt-get update \
 && apt-get install -y docker-ce
