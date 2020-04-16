# Molecule managed

# Ansible cloud tools for lab based deployments
# Copyright (C) 2020  Kevin Carter
#
# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <https://www.gnu.org/licenses/>.


{% if item.registry is defined %}
FROM {{ item.registry.url }}/{{ item.image }}
{% else %}
FROM {{ item.image }}
{% endif %}

RUN if [ $(command -v apt-get) ]; then apt-get update && apt-get install -y python sudo bash ca-certificates && apt-get clean; \
    elif [ $(command -v dnf) ]; then dnf makecache && dnf --assumeyes install sudo python*-devel python*-dnf bash {{ item.pkg_extras | default('') }} && dnf clean all; \
    elif [ $(command -v yum) ]; then yum makecache fast && yum install -y python sudo yum-plugin-ovl python-setuptools bash {{ item.pkg_extras | default('') }} && sed -i 's/plugins=0/plugins=1/g' /etc/yum.conf && yum clean all; \
    elif [ $(command -v zypper) ]; then zypper refresh && zypper install -y python sudo bash python-xml {{ item.pkg_extras | default('') }} && zypper clean -a; \
    elif [ $(command -v apk) ]; then apk update && apk add --no-cache python sudo bash ca-certificates {{ item.pkg_extras | default('') }}; \
    elif [ $(command -v xbps-install) ]; then xbps-install -Syu && xbps-install -y python sudo bash ca-certificates {{ item.pkg_extras | default('') }} && xbps-remove -O; fi

{% for pkg in item.easy_install | default([]) %}
# install pip for centos where there is no python-pip rpm in default repos
RUN easy_install {{ pkg }}
{% endfor %}


CMD ["sh", "-c", "while true; do sleep 10000; done"]
