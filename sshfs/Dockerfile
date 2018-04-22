# EXAMPLE :
# docker run --rm  -it -v `pwd`/tmp:/tmp -e "SSH_KEY=$YOUR_KEY" -e "SSH_USER=you" -e "SSH_SERVER=server" --privileged linuxidefix/ftp
FROM alpine:latest
ENV SSH_USER=""
ENV SSH_SERVER=""
ENV SSH_KEY=""

RUN apk update \
&& apk add --no-cache fuse \
&& apk add --no-cache sshfs \
&& mkdir -p $HOME/keys

ENTRYPOINT  [[ -n "$SSH_KEY" ]] && \ 
            [[ -n "$SSH_SERVER" ]] && \ 
            [[ -n "$SSH_USER" ]] && \ 
            echo "$SSH_KEY" > $HOME/keys/ssh_key && \
            chmod 600 $HOME/keys/ssh_key && \
            echo "`date` Connecting to $SSH_USER@$SSH_SERVER" |tee /tmp/startup.log && \
            mkdir -p /mnt/ftp/$SSH_USER && \
            sshfs -o allow_other,reconnect,ServerAliveInterval=15,ServerAliveCountMax=3,IdentityFile=$HOME/keys/ssh_key \
            -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null \ 
            $SSH_USER@$SSH_SERVER:/home/$SSH_USER /mnt/ftp/$SSH_USER && \
            echo "`date` Connected to $SSH_USER@$SSH_SERVER" |tee /tmp/startup.log && \
            ls -Rhl /mnt/ftp/$SSH_USER |tee /tmp/startup.log && \
            sh
