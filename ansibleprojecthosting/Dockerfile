# Gebruik de officiële Python-image als basis.
FROM python:3.9-slim

# Stel omgevingsvariabelen in.
ENV ANSIBLE_HOST_KEY_CHECKING=False

# Installeer systeemafhankelijkheden en Ansible.
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    build-essential \
    libssl-dev \
    libffi-dev \
    python3-dev \
    sshpass \
    openssh-client \
    && pip install --upgrade pip \
    && pip install ansible \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Maak de werkdirectory aan.
WORKDIR /ansible

# Kopieer het playbook, hosts-bestand, ansible.cfg en SSH-sleutel naar de container.
COPY . /ansible


# Stel de permissies in voor de SSH-sleutel.
RUN chmod 600 /ansible/id_rsa

# Stel omgevingsvariabele in voor de private sleutel.
ENV ANSIBLE_PRIVATE_KEY_FILE=/ansible/id_rsa

# Voer het playbook uit, -i wijst naar het hosts-bestand, main.yaml naar het playbook en -K vraagt om het wachtwoord voor de become-regel in de playbook.
CMD ["ansible-playbook", "-i", "hosts", "main.yml"]