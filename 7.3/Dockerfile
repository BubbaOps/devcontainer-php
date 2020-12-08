FROM bubbaops/baseimage-php:7.3

RUN DEBIAN_FRONTEND=noninteractive
RUN locale-gen en_US.UTF-8

ENV LANGUAGE=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8
ENV LC_CTYPE=en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV TERM xterm

ARG USER_PASSWORD=aStrong(!)Password
ENV USER_PASSWORD ${USER_PASSWORD}

ENV INTALL_PACKAGES \
        zsh \
		neovim \
		python3-neovim \
        git 

# Start as root
USER root

RUN set -xe \
    && apt-get update \
    && apt-get install -yqq  ${INTALL_PACKAGES} \
    && pecl channel-update pecl.php.net \
    && groupadd -g 1000 development \
    && useradd -u 1000 -g development -m developer -G sudo \
    && usermod -p $(openssl passwd -1 ${USER_PASSWORD}) developer -s /usr/bin/zsh

###########################################################################
# Set Timezone
###########################################################################

ARG TZ=UTC
ENV TZ ${TZ}

RUN  set -xe \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \
    && composer global require "laravel/installer"

USER developer
WORKDIR /home/developer

COPY zsh/p10k.zsh .p10k.zsh
COPY zsh/zshrc .zshrc
COPY zsh/aliases.zsh aliases.zsh

RUN set -xe \
    && sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" \
    && git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/.oh-my-zsh/custom/themes/powerlevel10k

ENV NVM_DIR /home/developer/.nvm

RUN set -xe \
    && mkdir -p $NVM_DIR \
    && curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash \
    && . $NVM_DIR/nvm.sh \
    && nvm install node --lts \
    && nvm use node \
    && npm install -g gulp \
    && npm install -g bower \
    && npm install -g @vue/cli \
    && npm install -g @angular/cli \
    && ln -s `npm bin --global` /home/developer/.node-bin 

ENV PATH $PATH:/home/laradock/.node-bin

RUN set -xe \
    && . "$NVM_DIR/nvm.sh" \
    && curl -o- -L https://yarnpkg.com/install.sh | bash


USER root
RUN set -xe \
    && find $NVM_DIR -type f -name node -exec ln -s {} /usr/local/bin/node \;  \
    && NODE_MODS_DIR="$NVM_DIR/versions/node/$(node -v)/lib/node_modules" \
    && ln -s $NODE_MODS_DIR/bower/bin/bower /usr/local/bin/bower  \
    && ln -s $NODE_MODS_DIR/gulp/bin/gulp.js /usr/local/bin/gulp  \
    && ln -s $NODE_MODS_DIR/npm/bin/npm-cli.js /usr/local/bin/npm  \
    && ln -s $NODE_MODS_DIR/npm/bin/npx-cli.js /usr/local/bin/npx  \
    && ln -s $NODE_MODS_DIR/vue-cli/bin/vue /usr/local/bin/vue  \
    && ln -s $NODE_MODS_DIR/vue-cli/bin/vue-init /usr/local/bin/vue-init  \
    && ln -s $NODE_MODS_DIR/vue-cli/bin/vue-list /usr/local/bin/vue-list

RUN set -xe \
    && apt-get -y install python python-pip python-dev  \
    && python -m pip install --upgrade pip  \
    && python -m pip install --upgrade virtualenv

# Clean up
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    rm /var/log/lastlog /var/log/faillog

WORKDIR /tmp
CMD ["/usr/bin/zsh"]