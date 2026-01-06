FROM alpine/git:latest AS addons-builder

WORKDIR /repos

RUN git clone --depth 1 -b 17.0 https://github.com/OCA/storage.git
RUN git clone --depth 1 -b 17.0 https://github.com/OCA/server-env.git

# etapa2
FROM odoo:17

USER root

RUN pip install --no-cache-dir fsspec s3fs boto3

COPY --from=addons-builder /repos/storage/fs_storage /mnt/extra-addons/fs_storage
COPY --from=addons-builder /repos/storage/fs_attachment /mnt/extra-addons/fs_attachment
COPY --from=addons-builder /repos/storage/fs_attachment_s3 /mnt/extra-addons/fs_attachment_s3
COPY --from=addons-builder /repos/server-env/server_environment /mnt/extra-addons/server_environment

RUN ls -la /mnt/extra-addons/

USER odoo
