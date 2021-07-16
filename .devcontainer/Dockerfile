FROM ubuntu:21.04

ARG USER_NAME="dev"
ARG USER_PASSWORD="dev"
ARG DB_HOST="postgres"
ARG REDIS_HOST="redis"

ENV USER_NAME=${USER_NAME}
ENV USER_PASSWORD=${USER_PASSWORD}
ENV DB_HOST=${DB_HOST}
ENV REDIS_HOST=${REDIS_HOST}

RUN \
  apt update && \
  apt upgrade -y && \
  apt install nano git curl zsh fonts-powerline fonts-firacode locales postgresql-client redis-tools -y && \
  locale-gen en_US.UTF-8 && \
  adduser --quiet --disabled-password --shell /bin/zsh --home "/home/${USER_NAME}" --gecos "User" ${USER_NAME} && \
  echo "${USER_NAME}:${USER_PASSWORD}" | chpasswd && usermod -aG sudo ${USER_NAME}

RUN curl -fsSL https://deb.nodesource.com/setup_14.x | bash -
RUN apt install nodejs

USER ${USER_NAME}

RUN sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
RUN cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
RUN echo "alias postgres=\"psql -h ${DB_HOST}\"" >> ~/.zshrc
RUN echo "alias redis=\"redis-cli -h ${REDIS_HOST}\"" >> ~/.zshrc
RUN sed -i 's/ZSH_THEME="robbyrussell"/ZSH_THEME="agnoster"/g' ~/.zshrc

CMD [ "zsh" ]