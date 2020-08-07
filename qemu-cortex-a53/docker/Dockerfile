# VERSION 1.0
FROM ljishen/qemu-arm
MAINTAINER Alex Bistagne <abistagn@ucsc.edu>

ENV VERSION 4.19.50
RUN apt-get install -y qemu-utils \
     && mv /root/system/qemu-rpi-kernel/kernel-qemu-${VERSION}-buster /root/system/qemu-rpi-kernel/kernel-qemu-buster
ENV KERNEL /root/system/qemu-rpi-kernel/kernel-qemu-buster     
ENV DTB /root/system/qemu-rpi-kernel/versatile-pb-buster.dtb     
ENV DRIVE_FILE /var/tmp/img/Rasbian.img
ENV STOP /var/tmp/img/stop
#expose /var/img to the outside

EXPOSE -P 5022
EXPOSE 1234 
#don't publish 1234

CMD ["sh", "-c", \
     " ( until test -f $DRIVE_FILE; do sleep 1; done && \
        qemu-system-arm \
        -kernel KERNEL \
        -cpu arm1176 \
        -m 256 \
        -M DTB \
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
        
