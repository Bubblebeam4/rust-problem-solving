FROM --platform=linux/amd64 mcr.microsoft.com/vscode/devcontainers/rust:latest

# Vivaldi install
RUN apt-get update && apt-get upgrade -y \
    && wget -qO- https://repo.vivaldi.com/archive/linux_signing_key.pub | gpg --dearmor | dd of=/usr/share/keyrings/vivaldi-browser.gpg \
    && echo "deb [signed-by=/usr/share/keyrings/vivaldi-browser.gpg arch=$(dpkg --print-architecture)] https://repo.vivaldi.com/archive/deb/ stable main" | dd of=/etc/apt/sources.list.d/vivaldi-archive.list \
    && apt-get update && apt-get install -y vivaldi-stable

# Desktop lite
COPY library-scripts/desktop-lite-debian.sh /tmp/library-scripts/
RUN apt-get update \
    && bash /tmp/library-scripts/desktop-lite-debian.sh \
    && chown -R vscode /home/vscode
ENV DBUS_SESSION_BUS_ADDRESS="autolaunch:" \
    VNC_RESOLUTION="1440x768x16" \
    VNC_DPI="96" \
    VNC_PORT="5901" \
    NOVNC_PORT="6080" \
    DISPLAY=":1" \
    LANG="en_US.UTF-8" \
    LANGUAGE="en_US.UTF-8"
ENTRYPOINT ["/usr/local/share/desktop-init.sh"]
CMD ["sleep", "infinity"]