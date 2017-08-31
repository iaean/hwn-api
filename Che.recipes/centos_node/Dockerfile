FROM eclipse/centos_jdk8
RUN sudo yum makecache fast && \
    sudo yum -y update && \
    sudo yum -y install epel-release centos-release-scl && \
    sudo yum -y install joe man net-tools nmap-ncat socat iproute telnet bind-utils cairo && \
    sudo yum clean all && \
    sudo sed -ri 's/^ -nobackups/-nobackups/g' /etc/joe/joerc && \
    echo -e '$include /etc/inputrc\n"\\ep": history-search-backward\n"\\en": history-search-forward' > /home/user/.inputrc

ENV NODE_VERSION v6.11.2
RUN wget -qO- https://nodejs.org/dist/${NODE_VERSION}/node-${NODE_VERSION}-linux-x64.tar.gz | sudo -E tar -C /opt -xvzf- && \
    sudo ln -s node-${NODE_VERSION}-linux-x64 /opt/nodejs && \
    sudo chown -R root:root /opt/nodejs/

USER root
ENV NODE_PATH /opt/nodejs/lib/node_modules
ENV PATH "/opt/nodejs/bin:${PATH}"

### RUN npm --user=root update -g # NOTE: breaks npm...

RUN npm --no-color --user=root install -g swagger swagger-ui \
  babel-cli bluebird bower yarn browserify \
  d3 deep-extend express express-generator \
  grunt-cli grunt gulp ipaddr.js elasticsearch memcached mysql \
  jquery jscs js-beautify jscs jshint jslint jsonfile json-server \
  uglify-js underscore underscore-db lodash uuid-1345 xlsx \
  request require lowdb netmask node-xlsx password-generator pm2 q >/dev/null

RUN npm --no-color --user=root install -g asyncflow common-node synchronize streamline >/dev/null

# RUN echo 'export PATH=/opt/nodejs/bin:$PATH' >> /root/.bash_profile
# RUN echo 'export NODE_PATH=/opt/nodejs/lib/node_modules' >> /root/.bash_profile
RUN echo 'export PATH=/opt/nodejs/bin:$PATH' >> /root/.bashrc
RUN echo 'export NODE_PATH=/opt/nodejs/lib/node_modules' >> /root/.bashrc

USER user
# RUN echo 'export PATH=/opt/nodejs/bin:$PATH' >> /home/user/.bash_profile
# RUN echo 'export NODE_PATH=/opt/nodejs/lib/node_modules' >> /home/user/.bash_profile
RUN echo 'export PATH=/opt/nodejs/bin:$PATH' >> /home/user/.bashrc
RUN echo 'export NODE_PATH=/opt/nodejs/lib/node_modules' >> /home/user/.bashrc

WORKDIR /projects
CMD tail -f /dev/null
