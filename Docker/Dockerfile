FROM ubuntu:latest

# Set n8n environment type ('dev' or 'stable'). It differs the logo shown in the UI.
ENV N8N_RELEASE_TYPE='stable'
ENV N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true
ENV N8N_RUNNERS_ENABLED=true

# Update and install dependencies
RUN apt update -y && apt upgrade -y && \
    apt install wget libaio1t64 curl alien -y

# Install Node.js 22 LTS using NodeSource repository
RUN curl -fsSL https://deb.nodesource.com/setup_lts.x | bash - && \
    apt-get install -y nodejs

# Install n8n and oracledb globally
RUN npm install n8n oracledb -g

# Create a node user
RUN addgroup --gid 1001 node && \
    adduser --uid 1001 --ingroup node --shell /bin/sh --disabled-password --gecos "" node && \
    export GNUPGHOME="$(mktemp -d)"

WORKDIR /tmp

# Get instantclient rpm files
RUN wget https://download.oracle.com/otn_software/linux/instantclient/oracle-instantclient-basic-linuxx64.rpm

# Install intantclient with Alien
RUN alien -i oracle-instantclient-basic-linuxx64.rpm

# Create a symbolic link from libaio.so.1t64 with libaio.so.1 - https://askubuntu.com/questions/1512196/libaio1-on-noble
RUN ln -s /usr/lib/x86_64-linux-gnu/libaio.so.1t64 /usr/lib/x86_64-linux-gnu/libaio.so.1

RUN rm oracle-instantclient-basic-linuxx64.rpm

# Create the folder and set the permissions
RUN mkdir -p /home/node/.n8n && chown -R node:node /home/node/.n8n

WORKDIR /app

USER node

EXPOSE 5678:5678

ENTRYPOINT ["n8n"]
