FROM odoo:17

USER root

RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    && rm -rf /var/lib/apt/lists/*

RUN pip install --no-cache-dir fsspec s3fs boto3

RUN git clone --depth 1 -b 17.0 https://github.com/OCA/storage.git /tmp/storage \
    && cp -R /tmp/storage/fs_storage /mnt/extra-addons/ \
    && cp -R /tmp/storage/fs_attachment /mnt/extra-addons/ \
    && cp -R /tmp/storage/fs_attachment_s3 /mnt/extra-addons/ \
    && rm -rf /tmp/storage

RUN git clone --depth 1 -b 17.0 https://github.com/OCA/server-env.git /tmp/server-env \
    && cp -R /tmp/server-env/server_environment /mnt/extra-addons/ \
    && rm -rf /tmp/server-env

RUN ls -la /mnt/extra-addons/

USER odoo

