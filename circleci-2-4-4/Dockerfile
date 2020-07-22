FROM circleci/ruby:2.4.4-browsers

RUN sudo apt update
RUN sudo apt install -y libgtk-3-0
RUN sudo apt install -y openjdk-8-jre-headless
RUN sudo wget http://selenium-release.storage.googleapis.com/2.53/selenium-server-standalone-2.53.1.jar

RUN curl -sL https://deb.nodesource.com/setup_8.x | sudo bash
RUN sudo apt install -y nodejs
RUN sudo npm install -g yarn

RUN sudo java -jar selenium-server-standalone-2.53.1.jar &
