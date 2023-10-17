FROM alpine:3.16

WORKDIR /var/hugo/static

RUN apk update && apk upgrade && apk add --update --no-cache \
	hugo git shadow \
	&& rm -f /var/cache/apk/*

RUN hugo new site /var/hugo/static \
	&& cd /var/hugo/static \
	&& git clone https://github.com/LordMathis/hugo-theme-nightfall themes/nightfall \
	&& hugo new posts/adminer.md \
	&& hugo -b https://tcelik.42.fr/static \
	&& mkdir -p /var/hugo/info/content/posts

# conf/ dizininde hugoda kullanılacak markdown dosyaları ve config dosyası bulunmakta
COPY ./conf/config.toml /var/hugo/static/config.toml
COPY conf/adminer.md    /var/hugo/static/content/posts/adminer.md
COPY conf/about.md      /var/hugo/static/content/about/index.md
COPY conf/1.png         /var/hugo/static/themes/nightfall/static/1.png
COPY conf/2.png         /var/hugo/static/themes/nightfall/static/2.png

EXPOSE 1313

CMD ["hugo", "server", \
	"--bind=0.0.0.0", \
	"--baseURL=https://tcelik.42.fr/static", \
	"-p", "1313", \
	"--logFile=/dev/stdout", \
	"--appendPort=false"]
