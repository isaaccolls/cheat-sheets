# config

Dispositivo: tracker genérico OEM (misma familia que "Dyegoo GT02A", manual "User Manual Version 2.3", plataforma gps.dyegoo.net). Contraseña por defecto: `666666`.

Lista de comandos SMS **completa y confirmada** contra el manual oficial de fábrica (no la cheat-sheet genérica que había antes, que era de otro protocolo/tracker y por eso no funcionaba):

1. `PASSWORD,vieja_clave,nueva_clave#` — cambiar contraseña (default 666666) 👈
2. `RECOVER,nueva_clave#` — restablecer la clave a la de fábrica (666666)
3. `SERVER,666666,modo,IP_o_dominio,puerto,0#` — modo 0=IP, 1=DNS/dominio
4. `APN,666666,nombre_apn,usuario_apn,clave_apn#` — usuario/clave solo si el APN los requiere, si no se omiten
5. `WHERE,666666#` — consulta posición GPS (responde Lat/Lon/Course/Speed/DateTime)
6. `URL,666666#` — enlace de Google Maps con la posición actual 👈
7. `TIMER,666666,,segundos#` — intervalo de subida de posición (5–1800s, default 10s) (set 50)
8. `GMT,666666,E_o_W,codigo#` — huso horario
9. `FACTORY,666666#` — reset de fábrica (NO borra IP/puerto/DNS/clave)

## initial

1. set apn: `APN,666666,APN#`
1. set server: `SERVER,666666,1,gps.dyegoo.net,6100,0#`
1. set timer: `timer,666666,,15#`
