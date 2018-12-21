# fzf in a docker container.
# also fzf is really slow like this.

FROM golang:alpine as builder

RUN apk --update add \
	git \
	automake \ 
	autoconf \
	make \
	g++ \
	curl \
	bash \
	pcre-dev xz-dev

RUN git clone --depth 1 \
	https://github.com/junegunn/fzf.git \
	~/.fzf

RUN git clone --depth 1 --single-branch --branch 2.0.0 \
	https://github.com/ggreer/the_silver_searcher.git \
	~/the_silver_searcher

RUN ~/the_silver_searcher/build.sh && \
	~/.fzf/install

FROM alpine:latest

ENV FZF_DEFAULT_COMMAND '/root/ag -g "" /tmp'

RUN apk --update add pcre-dev xz-dev
COPY --from=builder /root/.fzf/bin/fzf /root/fzf
COPY --from=builder /root/the_silver_searcher/ag /root/ag

CMD [ "/root/fzf" ]