## Dockerfile for a haskell environment
FROM       ubuntu:latest
MAINTAINER AJ

## ensure locale is set during build
ENV LANG            C.UTF-8

RUN echo 'deb http://ppa.launchpad.net/hvr/ghc/ubuntu trusty main' > /etc/apt/sources.list.d/ghc.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys F6F88286 && \
    apt-get update && \
    apt-get install -y --no-install-recommends cabal-install-1.20 ghc-7.8.4 ghc-7.8.4-htmldocs happy-1.19.4 
	    alex-3.1.3 webfs zlib1g-dev git vim libtinfo-dev libsqlite3-0 libsqlite3-dev && \
    rm -rf /var/lib/apt/lists/*

ENV PATH /root/.cabal/bin:/opt/cabal/1.20/bin:/opt/ghc/7.8.4/bin:/opt/happy/1.19.4/bin:/opt/alex/3.1.3/bin:.cabal-sandbox/bin:$PATH

WORKDIR /root

RUN git clone https://github.com/ajjaic/Configs.git && \
    cp Configs/vimrc.haskell .vimrc && \
    git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim && \
    vim +PluginInstall +qall now

WORKDIR .vim/bundles/vimproc.vim

RUN make

## run ghci by default unless a command is specified
CMD ["ghci"]
