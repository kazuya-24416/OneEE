FROM nvcr.io/nvidia/pytorch:24.01-py3
ENV UID 20033

# install essential softwares
# RUN if [ -e /etc/apt/sources.list.d/cuda.list ] ; then rm /etc/apt/sources.list.d/cuda.list; fi ; apt update
RUN apt update
RUN DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC apt-get -y install tzdata
RUN apt install -y vim zsh git ssh sudo language-pack-en tmux libssl-dev libmysqlclient-dev sqlite3 build-essential
RUN update-locale LANG=en_US.UTF-8
RUN python -m pip install --upgrade pip
RUN python -m pip install setuptools packaging

RUN apt update && apt install -y curl
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y
ENV PATH="/root/.cargo/bin:${PATH}"

COPY requirements.txt /workspace/requirements.txt
RUN python -m pip install -r /workspace/requirements.txt

RUN yes | adduser --uid $UID --shell /usr/bin/zsh --disabled-password user -q
RUN ln -s /workspace /home/user/workspace && chown user:user /workspace && chmod 755 /workspace
USER user
WORKDIR /workspace