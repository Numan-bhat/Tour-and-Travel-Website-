FROM python:3.12-slim

ENV PYTHONUNBUFFERED=1 \
    PORT=8080

WORKDIR /app

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

COPY . ./
RUN useradd --create-home --shell /usr/sbin/nologin appuser \
    && mkdir -p /app/instance /app/static/uploads \
    && chown -R appuser:appuser /app

USER appuser
EXPOSE 8080

CMD ["sh", "-c", "exec waitress-serve --url-scheme=https --host=0.0.0.0 --port=${PORT:-8080} wsgi:application"]
