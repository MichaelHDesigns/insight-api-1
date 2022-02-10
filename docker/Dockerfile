FROM node:8-alpine

RUN apk add --update --no-cache \
                            git \
                            libzmq \
                            zeromq-dev \
                            python \
                            make \
                            g++

WORKDIR /insight

# Copy helpthehomeless-node
RUN git clone --branch master --single-branch --depth 1 https://github.com/Altcoin-Cash/helpthehomeless-node.git .

# Copy config file
COPY helpthehomeless-node.json .

ARG VERSION

# Install npm packages
RUN npm ci

# Install Insight API module
RUN bin/helpthehomeless-node install @Altcoin-Cash/insight-api@${VERSION}

FROM node:8-alpine

LABEL maintainer="Helpthehomeless Developers <dev@helpthehomeless.org>"
LABEL description="Dockerised Insight API"

WORKDIR /insight

# Copy project files
COPY --from=0 /insight/ .

EXPOSE 3001

CMD ["bin/helpthehomeless-node", "start"]
