# Run spotify in a container
#

FROM debian:latest


RUN apt-get update && apt-get -y upgrade \
    && apt install -y dirmngr gnupg --no-install-recommends \
    && apt-key  adv --keyserver keyserver.ubuntu.com --recv-keys 0DF731E45CE24F27EEEB1450EFDC8610341D9410 931FF8E79F0876134EDDBDCCA87FF9DF48BF1C90 \
    && echo deb http://repository.spotify.com stable non-free >> /etc/apt/sources.list.d/spotify.list \
    && apt-get update && apt-get install -y \
    alsa-utils \
    libgl1-mesa-dri \
    libgl1-mesa-glx \
    spotify-client \
    xdg-utils \
    --no-install-recommends \
    && rm -rf /var/lib/apt/lists/*
    
ENV HOME /home/spotify
RUN useradd --create-home --home-dir $HOME spotify \
    && gpasswd -a spotify audio \
    && chown -R spotify:spotify $HOME

WORKDIR $HOME
USER spotify

# make search bar text better
RUN echo "QLineEdit { color: #000 }" > /home/spotify/spotify-override.css

ENTRYPOINT  [ "spotify" ]
CMD [ "-stylesheet=/home/spotify/spotify-override.css" ]

