# Decisiones

Formato: qué se decidió, por qué, y qué alternativa se descartó.

## D-001 — Ansible en lugar de scripts propios

- **Decisión:** Ansible como herramienta de configuración.
- **Motivo:** es declarativo e idempotente, no requiere agente en el objetivo y
  es el estándar en operación de sistemas Linux.
- **Alternativa descartada:** scripts de Bash con `set -e`; funcionan una vez y
  luego hay que inventar a mano la detección de cambios.

## D-002 — La idempotencia es el criterio de terminado

- **Decisión:** el proyecto no está listo hasta que la segunda ejecución dé
  `changed=0`.
- **Motivo:** demuestra que el playbook describe un estado, no una secuencia de
  comandos. Es la propiedad que se rompe primero cuando alguien "arregla" un
  playbook a las apuradas.
- **Consecuencia:** cada tarea debe tener una condición o un módulo que sepa
  medir el estado actual.

## D-003 — El controlador no se endurece a sí mismo

- **Decisión:** en v0.1 `lab-control` ejecuta el playbook sobre `lab-app`; no se
  aplica a sí mismo.
- **Motivo:** una regla de SSH mal escrita sobre el controlador corta la sesión
  que se está usando y deja el playbook a medio aplicar.
- **Alternativa descartada:** aplicarlo primero al controlador; se hará después,
  con una sesión de consola abierta como red de seguridad.
