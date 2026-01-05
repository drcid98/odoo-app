FROM alpine/git:latest AS addons-builder

WORKDIR /addons

RUN git clone --depth 1 -b 17.0 https://github.com/OCA/storage.git /tmp/storage \
    && cp -R /tmp/storage/fs_storage . \
    && cp -R /tmp/storage/fs_attachment . \
    && cp -R /tmp/storage/fs_attachment_s3 . \
    && rm -rf /tmp/storage

RUN git clone --depth 1 -b 17.0 https://github.com/OCA/server-env.git /tmp/server-env \
    && cp -R /tmp/server-env/server_environment . \
    && rm -rf /tmp/server-env

FROM odoo:17

USER root

RUN pip install --no-cache-dir fsspec s3fs boto3

COPY --from=addons-builder /addons /mnt/extra-addons/

RUN ls -la /mnt/extra-addons/

USER odoo
