# Original from https://support.nordvpn.com/hc/en-us/articles/20465811527057-How-to-build-the-NordVPN-Docker-image
FROM ubuntu:24.04

ENV nord_vpn_token = ""
ENV nord_vpn_server = ""
ENV torrent_webui_port = ""

# Setup NordVPN Package
RUN apt-get update && \
apt-get install -y --no-install-recommends wget apt-transport-https ca-certificates && \
    apt-get install -y --no-install-recommends wget apt-transport-https ca-certificates && \ 
    wget -qO /etc/apt/trusted.gpg.d/nordvpn_public.asc https://repo.nordvpn.com/gpg/nordvpn_public.asc && \
    echo "deb https://repo.nordvpn.com/deb/nordvpn/debian stable main" > /etc/apt/sources.list.d/nordvpn.list && \
    apt-get update && \
    apt-get install -y --no-install-recommends nordvpn && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

ENTRYPOINT /etc/init.d/nordvpn start && \
    sleep 5 && \
    nordvpn login --token "${nord_vpn_token}" && \
    nordvpn whitelist add port ${torrent_webui_port} && \
    nordvpn connect "${nord_vpn_server}" && \
    nordvpn status && \
    tail -f /dev/null