# linux-baseline

[English version](README.en.md)

Baseline de seguridad para las máquinas virtuales del laboratorio, aplicado con
Ansible y verificado por idempotencia. Una VM recién clonada pasa a un estado
endurecido y comprobable, sin importar cuántas veces se ejecute el playbook.

Parte del laboratorio descrito en
[homelab](https://github.com/jossan-sj8/homelab).

## Estado

Fase 0 — repositorio y alcance definidos.

## Objetivo

Que la segunda ejecución del playbook no cambie nada (`changed=0`). Esa es la
diferencia entre un script y una declaración de estado.

## Alcance de v0.1

- SSH: sólo llaves, sin acceso de root, timeouts y límite de intentos.
- `sudo`: registro de cada uso en el journal.
- `firewalld`: sólo los servicios necesarios, declarados en el playbook.
- SELinux: `Enforcing` verificado, no supuesto.
- `auditd`: reglas mínimas (ejecución de comandos, cambios de identidad).
- Sincronización de hora (`chrony`) y zona horaria.
- Informe antes/después por host.

## Fuera de alcance

- Cumplimiento CIS completo.
- Integración con LDAP o directorio corporativo.
- Backups (corresponde a `homelab` con `vzdump`).

## Inventario

| Host | IP | Rol en Ansible |
|---|---|---|
| `lab-control` | `192.168.1.50` | controlador |
| `lab-app` | `192.168.1.51` | objetivo |

## Cómo se ejecuta

_pendiente: se escribe cuando exista el primer playbook._

## Definition of done

- Segunda ejecución del playbook con `changed=0`.
- Informe antes/después por host.
- Diferencias de `sshd_config` y de firewall documentadas.
- README bilingüe y runbook actualizado.

## Seguridad

- El playbook no abre puertos: sólo cierra y declara los existentes.
- Ningún cambio de SSH se aplica sin probar antes una sesión nueva.
- Los cambios de `sshd` incluyen una prueba de reversión con `qm terminal`.

## Documentos

- [PROGRESO_LAB.md](PROGRESO_LAB.md) — estado actual y próximo paso.
- [DECISIONES.md](DECISIONES.md) — qué se eligió y por qué.
- [ERRORES.md](ERRORES.md) — fallos, causa raíz, cómo evitarlos.
