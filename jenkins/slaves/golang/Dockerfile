FROM jenkins/jnlp-slave

user root
# docker
RUN apt-get update
RUN apt-get -y install apt-transport-https ca-certificates curl gnupg2 software-properties-common
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"

RUN apt-get update
RUN apt-get -y install docker-ce

# golang go1.13.10
RUN wget https://dl.google.com/go/go1.13.10.linux-amd64.tar.gz
RUN tar -xvf go1.13.10.linux-amd64.tar.gz

RUN mv go /usr/local/bin/
RUN mkdir /usr/local/go

# gcloud
RUN curl https://dl.google.com/dl/cloudsdk/release/google-cloud-sdk.tar.gz > /tmp/google-cloud-sdk.tar.gz
RUN mkdir -p /usr/local/gcloud \
  && tar -C /usr/local/gcloud -xvf /tmp/google-cloud-sdk.tar.gz \
  && /usr/local/gcloud/google-cloud-sdk/install.sh

ENV GOROOT=/usr/local/bin/go
ENV GOPATH=/usr/local/go
ENV PATH=${GOPATH}/bin:${GOROOT}/bin:${PATH}
ENV PATH $PATH:/usr/local/gcloud/google-cloud-sdk/bin

RUN gcloud components install kubectl
RUN go get -u honnef.co/go/tools/cmd/staticcheck
RUN go version
RUN gcloud version
RUN git config --global url."git@github.com:".insteadOf "https://github.com/"
RUN apt-get install -y php

RUN apt-install -y openvpn