# Procedimiento: Instalación de Nodos de Bitcoin para Comercios

## 1. Introducción y Beneficios

Un nodo de Bitcoin es un programa que descarga y verifica de forma independiente toda la blockchain, validando cada transacción y bloque contra las reglas de consenso de la red. Para un comercio, operar un nodo propio ofrece beneficios concretos:

- **Independencia de terceros**: El negocio verifica sus propias transacciones sin depender de servidores públicos o procesadores externos.
- **Mayor privacidad**: Se reduce la información compartida con servicios de terceros.
- **Integración con sistemas de pago**: El nodo puede conectarse a plataformas como BTCPay Server, Tiankii o LNbits para aceptar pagos en Bitcoin y Lightning Network directamente en el punto de venta.

---

## 2. Requisitos Previos

### 2.1 Hardware Recomendado

| Componente | Mínimo | Recomendado |
|---|---|---|
| CPU | 2 vCPU | 4 núcleos o más |
| RAM | 4 GB | 8 GB o superior |
| Almacenamiento | 1 TB SSD | 1 TB SSD (para nodo completo) |
| Conexión | Banda ancha estable | Fibra óptica con IP fija |
| Energía | UPS básico | UPS + respaldo |

La blockchain de Bitcoin supera actualmente los 650 GB y crece aproximadamente 80 GB al año, por lo que se recomienda un SSD de al menos 1 TB para un nodo completo.

### 2.2 Software Necesario

- **Bitcoin Core v25.0 o superior** (obligatorio)
- Sistema operativo: **Ubuntu 22.04 LTS o 24.04 LTS** (recomendado para servidores de comercio)
- Opcional: **BTCPay Server** o **LNbits** para gestión de pagos comerciales

---

## 3. Instalación Paso a Paso

### Paso 1: Preparar el Servidor

```bash
# Actualizar el sistema
sudo apt update && sudo apt upgrade -y

# Crear directorios necesarios
sudo mkdir -p /bitcoin/mainnet
sudo mkdir -p /etc/bitcoin

# Crear usuario dedicado (no usar root)
sudo useradd bitcoin -d /bitcoin
sudo chown -R bitcoin:bitcoin /bitcoin /etc/bitcoin/
```

Es fundamental ejecutar el nodo con un usuario sin privilegios administrativos.

### Paso 2: Descargar y Verificar Bitcoin Core

```bash
# Descargar desde el sitio oficial
wget https://bitcoincore.org/bin/bitcoin-core-25.0/bitcoin-25.0-x86_64-linux-gnu.tar.gz

# Verificar la firma GPG (CRÍTICO para seguridad)
gpg --verify bitcoin-25.0-x86_64-linux-gnu.tar.gz.sig

# Extraer e instalar
tar -xzf bitcoin-25.0-x86_64-linux-gnu.tar.gz
sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-25.0/bin/*
```

### Paso 3: Configurar Bitcoin Core

Crear el archivo `/etc/bitcoin/bitcoin.conf`:

```ini
# Directorio de datos
datadir=/bitcoin/mainnet

# RPC (solo acceso local por seguridad)
server=1
rpcallowip=127.0.0.1
rpcbind=127.0.0.1:8332
rpcauth=btcuser:hash_generado_con_script_oficial

# Red P2P
bind=127.0.0.1:8333

# Rendimiento
dbcache=4096
maxmempool=300

# No almacenar transacciones más de 24 horas
mempoolexpiry=24
```

El hash de `rpcauth` se genera con el script oficial de Bitcoin Core.

### Paso 4: Configurar el Servicio systemd

Crear `/etc/systemd/system/bitcoind.service`:

```ini
[Unit]
Description=Bitcoin Core Daemon
After=network.target

[Service]
User=bitcoin
Group=bitcoin
Type=forking
ExecStart=/usr/local/bin/bitcoind -daemon -conf=/etc/bitcoin/bitcoin.conf
ExecStop=/usr/local/bin/bitcoin-cli -conf=/etc/bitcoin/bitcoin.conf stop
Restart=on-failure
RestartSec=60

[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl enable --now bitcoind
```

### Paso 5: Configurar Firewall y Red

```bash
# Abrir puerto P2P para contribuir a la red
sudo ufw allow 8333/tcp

# Mantener RPC cerrado (solo local)
sudo ufw deny 8332/tcp

# Habilitar firewall
sudo ufw enable
```

Es importante exponer únicamente el puerto 8333 (P2P) y mantener el RPC (8332) estrictamente cerrado al exterior.

### Paso 6: Sincronización Inicial

```bash
# Verificar estado de sincronización
bitcoin-cli -conf=/etc/bitcoin/bitcoin.conf getblockchaininfo

# Monitorear progreso
tail -f /bitcoin/mainnet/debug.log
```

La sincronización inicial puede tardar **varios días**. Una vez completada, el nodo estará operativo.

---

## 4. Seguridad Avanzada

Para un entorno comercial, se recomienda aplicar las siguientes medidas adicionales:

| Medida | Configuración |
|---|---|
| **Modo blocksonly** | `blocksonly=1` — reduce el ancho de banda deshabilitando la retransmisión de transacciones |
| **Límite de subida** | `maxuploadtarget=5000` — limita el tráfico saliente diario a 5 GB |
| **Límite de mempool** | `maxmempool=300` — restringe el uso de memoria |
| **Nodo cortafuegos** | Ejecutar un segundo nodo interno que solo se conecte al exterior, protegiendo sistemas sensibles |

---

## 5. Integración con el Comercio

Una vez sincronizado el nodo, el comercio puede integrarlo con su punto de venta:

1. **BTCPay Server**: Desplegar mediante Docker y conectar al nodo Bitcoin Core local para procesar pagos en cadena y Lightning.
2. **Tiankii**: Plataforma de autcustodia que transforma cualquier billetera o nodo Lightning en un sistema POS completo con enlaces de pago, botones y gestión de sub-cuentas.
3. **LNbits**: Interfaz ligera para gestionar pagos Lightning desde el nodo propio, ideal para comercios pequeños.

---

## 6. Mantenimiento

- **Actualizaciones**: Verificar nuevas versiones de Bitcoin Core cada 3–6 meses.
- **Respaldos**: Guardar el archivo `bitcoin.conf` y las claves RPC en un lugar seguro.
- **Monitorización**: Revisar periódicamente el estado del nodo con `bitcoin-cli getnetworkinfo`.
- **Uptime**: Mantener el nodo encendido de forma continua para no perder sincronización ni canales Lightning.

---

## 7. Conclusión

Instalar un nodo de Bitcoin en un comercio es una inversión en **soberanía financiera y privacidad**. Aunque requiere una configuración técnica inicial, herramientas como BTCPay Server y Tiankii simplifican enormemente la integración con puntos de venta, permitiendo aceptar pagos en Bitcoin y Lightning Network sin depender de intermediarios. Con el hardware adecuado y las medidas de seguridad descritas, cualquier comercio puede operar su propia infraestructura de pagos descentralizada.