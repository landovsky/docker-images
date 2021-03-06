FROM ruby:2.3.7

# XVFB
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs qt5-default libqt5webkit5-dev xvfb

# Chromedriver whole setup (TODO: get CHROME_DRIVER_VERSION from chromedriver.storage.googleapis.com/LATEST_RELEASE)
ENV CHROME_DRIVER_VERSION=2.33 \
    SELENIUM_STANDALONE_VERSION=3.4.0 \
    SELENIUM_SUBDIR=3.4

# TODO: get SELENIUM_STANDALONE_VERSION like so: $(echo "$SELENIUM_STANDALONE_VERSION" | cut -d"." -f-2)

## CHROME
RUN apt-get -y install chromium \
 && wget -N https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb -P ~/ \
 && dpkg -i --force-depends ~/google-chrome-stable_current_amd64.deb \
 && apt-get -f install -y \
 && dpkg -i --force-depends ~/google-chrome-stable_current_amd64.deb

## SELENIUM
RUN wget -N http://selenium-release.storage.googleapis.com/$SELENIUM_SUBDIR/selenium-server-standalone-$SELENIUM_STANDALONE_VERSION.jar -P ~/
RUN mv -f ~/selenium-server-standalone-$SELENIUM_STANDALONE_VERSION.jar /usr/local/bin/selenium-server-standalone.jar
RUN chown root:root /usr/local/bin/selenium-server-standalone.jar
RUN chmod 0755 /usr/local/bin/selenium-server-standalone.jar

# Set the locale
RUN apt-get clean && apt-get update && apt-get install -y locales \
  && sed -i -e 's/# cs_CZ.UTF-8 UTF-8/cs_CZ.UTF-8 UTF-8/' /etc/locale.gen && locale-gen

ENV LANG cs_CZ.UTF-8 \
    LANGUAGE en_US:en \
    LC_ALL cs_CZ.UTF-8

RUN apt-get autoremove -y

RUN gem install bundler

ENV GEM_PATH=/root/.gem

CMD ["bash"]
