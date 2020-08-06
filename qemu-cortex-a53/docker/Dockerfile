# VERSION 1.0
FROM ljishen/qemu-arm
MAINTAINER Alex Bistagne <abistagn@ucsc.edu>

#code from my job at RREES lab
RUN apt-get intall -y qemu-utils \
     && curl https://codeload.github.com/dhruvvyas90/qemu-rpi-kernel/zip/master > kernel.zip \
     && unzip kernel.zip -d /tmp \
     && mv /tmp/*/kernel-qemu-*-buster /tmp/kernel-buster \
     && mv /tmp/*/versatile-pb-buster.dtb /tmp/versatile.dtb 
     
ENV DRIVE_FILE /var/tmp/img/Rasbian.img
ENV STOP /var/tmp/img/stop
#expose /var/img to the outside

EXPOSE -P 5022
EXPOSE 1234 
#don't publish 1234

CMD ["sh", "-c", \
     " ( until test -f $DRIVE_FILE; do sleep 1; done && \
        qemu-system-arm \
        -kernel /tmp/kernel-buster \
        -cpu arm1176 \
        -m 256 \
        -M /tmp/versatilepb \
        -append "root=/deb/sda2 rootfstype=ext4 rw" \
        -hda $DRIVE_FILE \
        -nographic \
        -net nic \
        -net user,hostfwd=tcp::5022-:22 \
        -dtb versatile.dtb \
        -no-shutdown \
        -monitor telnet:127.0.0.1:1234,server,nowait ) & \
     ( until test -f $STOP; \
          do sleep 1; \
          done && \
          telnet 127.0.0.1 1234 && \
          commit && \
          q ) "] 
        
