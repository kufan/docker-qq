FROM bestwu/wine:i386
LABEL maintainer='Peter Wu <piterwu@outlook.com>'

RUN apt-get update && \
    apt-get install -y --no-install-recommends deepin.com.qq.im && \
    apt-get -y autoremove --purge && apt-get autoclean -y && apt-get clean -y && \
    find /var/lib/apt/lists -type f -delete && \
    find /var/cache -type f -delete && \
    find /var/log -type f -delete && \
    find /usr/share/doc -type f -delete && \
    find /usr/share/man -type f -delete

ENV APP=QQ \
    AUDIO_GID=63 \
    VIDEO_GID=39 \
    GID=1000 \
    UID=1000

RUN groupadd -o -g $GID qq && \
    groupmod -o -g $AUDIO_GID audio && \
    groupmod -o -g $VIDEO_GID video && \
    useradd -d "/home/qq" -m -o -u $UID -g qq -G audio,video qq && \
    mkdir /TencentFiles && \
    chown -R qq:qq /TencentFiles && \
    ln -s "/TencentFiles" "/home/qq/Tencent Files"

VOLUME ["/TencentFiles"]

ADD entrypoint.sh /
ADD run.sh /
RUN chmod +x /entrypoint.sh && \
    chmod +x /run.sh
ENTRYPOINT ["/entrypoint.sh"]