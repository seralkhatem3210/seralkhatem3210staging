# /opt/odoo/staging/docker/Dockerfile
FROM odoo:18.0

USER root
RUN apt-get update && apt-get install -y --no-install-recommends \
    fonts-noto fonts-noto-cjk locales \
  && rm -rf /var/lib/apt/lists/*

# ✅ حل PEP 668
ENV PIP_BREAK_SYSTEM_PACKAGES=1

# تبعيات بايثون
COPY requirements.txt /tmp/requirements.txt
RUN python3 -m pip install --no-cache-dir -r /tmp/requirements.txt

# الإضافات والتهيئة
COPY addons /mnt/extra-addons
COPY docker/odoo.conf /etc/odoo/odoo.conf
COPY docker/entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh && chown -R odoo:odoo /mnt/extra-addons

USER odoo
ENTRYPOINT ["/entrypoint.sh"]
CMD ["odoo", "-c", "/etc/odoo/odoo.conf"]
