# Clave

Aplicación web de mensajería instantánea con cifrado de extremo a extremo,
desarrollada para el curso de Ética y Seguridad de Datos.

El navegador cifra y firma cada mensaje antes de enviarlo. El backend autentica
usuarios, conserva sobres cifrados y los entrega en tiempo real o cuando el
destinatario vuelve a conectarse, sin recibir el texto legible ni las claves
privadas.

## Componentes

- Backend en Python con FastAPI y SQLite.
- Cliente web sin frameworks externos.
- X25519, HKDF-SHA-256 y AES-256-GCM para el cifrado.
- Ed25519 para autenticar los sobres.
- HTTPS y WSS para proteger el transporte.
- Entrega asíncrona, deduplicación y confirmaciones ACK.

## Desarrollo local

Requiere Python 3.12 o 3.13, OpenSSL y un navegador con soporte para Web
Crypto, X25519 y Ed25519.

```bash
python3.13 -m venv .venv
.venv/bin/python -m pip install -r requirements.txt
cp .env.example .env
```

Cuando los scripts operativos estén incorporados, genera los certificados y
arranca el servicio:

```bash
./scripts/generate_certs.sh
.venv/bin/uvicorn app.main:app \
  --host 0.0.0.0 --port 8443 --env-file .env \
  --ssl-keyfile certs/server.key.pem \
  --ssl-certfile certs/server-chain.pem
```

Abre `https://localhost:8443` después de confiar en la CA del laboratorio.

## Equipo

- Vasco Diaz Hurtado
- Enzo Gomez Villegas
- Bladimir Alferez Vicente

## Sitio del proyecto

La presentación pública se despliega mediante GitHub Pages:

<https://vasc0d.github.io/Clave-Mensajeria-Segura/>

## Alcance

Este repositorio contiene la implementación del proyecto actual. No incluye el
prototipo heredado del curso anterior, bases de datos locales, certificados,
secretos ni el informe entregable del equipo.
