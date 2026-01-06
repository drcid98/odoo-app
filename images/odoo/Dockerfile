FROM alpine/git:latest AS addons-builder

# WORKDIR /addons

# esto hacerlo mas ordenado sin los cp
# RUN git clone --depth 1 -b 17.0 https://github.com/OCA/storage.git /tmp/storage \
#     && cp -R /tmp/storage/fs_storage . \
#     && cp -R /tmp/storage/fs_attachment . \
#     && cp -R /tmp/storage/fs_attachment_s3 . \
#     && rm -rf /tmp/storage

RUN git clone --depth 1 -b 17.0 https://github.com/OCA/storage.git /tmp/storage

# RUN git clone --depth 1 -b 17.0 https://github.com/OCA/server-env.git /tmp/server-env \
#     && cp -R /tmp/server-env/server_environment . \
#     && rm -rf /tmp/server-env
RUN git clone --depth 1 -b 17.0 https://github.com/OCA/server-env.git /tmp/server-env

# etapa2
FROM odoo:17

USER root

RUN pip install --no-cache-dir fsspec s3fs boto3

COPY --from=addons-builder /tmp/storage/fs_storage /mnt/extra-addons/fs_storage
COPY --from=addons-builder /tmp/storage/fs_attachment /mnt/extra-addons/fs_attachment
COPY --from=addons-builder /tmp/storage/fs_attachment_s3 /mnt/extra-addons/fs_attachment_s3
COPY --from=addons-builder /tmp/server-env/server_environment /mnt/extra-addons/server_environment

RUN ls -la /mnt/extra-addons/

USER odoo
