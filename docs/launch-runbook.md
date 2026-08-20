# Runbook de lanzamiento y distribución

Este documento deja preparada la publicación de **PropFácil MCP** en el Official MCP Registry y
los principales directorios. El backend ya está alojado; los catálogos deben apuntar al endpoint
remoto y nunca intentar construir el backend privado desde este repositorio.

Fuentes revisadas el **20 de agosto de 2026**:

- [Official MCP Registry: servidores remotos](https://modelcontextprotocol.io/registry/remote-servers)
- [Official MCP Registry: GitHub Actions](https://modelcontextprotocol.io/registry/github-actions)
- [Official MCP Registry: versionado](https://modelcontextprotocol.io/registry/versioning)
- [Smithery: publicar por URL](https://smithery.ai/docs/build/publish)
- [Cline MCP Marketplace: proceso de envío](https://github.com/cline/mcp-marketplace)

El Registry oficial sigue en preview. La metadata de una versión publicada no se reemplaza: cualquier
corrección exige una versión nueva. El CLI actual permite cambiar el estado de una release a
`deprecated` o `deleted`; por eso el tag se crea sólo después de aprobar el checklist “go/no-go”.

## Estado actual

| Componente | Estado antes del lanzamiento |
|---|---|
| Repositorio público | Listo: `https://github.com/jonatanvazquez/propfacil-mcp` |
| Endpoint remoto | Listo: `https://www.propfacil.com/api/mcp` |
| `server.json` | Válido ante la API oficial, nombre `io.github.jonatanvazquez/propfacil`, versión `1.3.8` |
| Workflow de validación | Listo y probado en `main` |
| Workflow del Registry | Listo; se activa con un tag `v*` o manualmente |
| Assets y textos | Listos en `assets/` y `directory-profile.json` |
| Instrucciones de instalación | Listas en README, `docs/installation.md` y `llms-install.md` |
| Publicación en catálogos | Registry oficial activo y Cline enviado; los demás estados están en el registro de lanzamiento |

## Go/no-go

No publicar hasta que todos los puntos siguientes estén completos:

- [ ] La versión desplegada del MCP coincide con `server.json` y con el tag que se creará.
- [ ] La revisión exacta del backend está en `main`, en GitHub y desplegada en producción.
- [ ] `initialize` y `tools/list` funcionan desde una red externa.
- [ ] Búsqueda, detalle, contacto y widget pasan sin autenticación.
- [ ] OAuth funciona desde un cliente MCP externo para favoritos y publicación.
- [ ] Website, documentación, privacidad, términos, soporte, server card e iconos responden por HTTPS.
- [ ] GitHub Actions **Validate distribution** está verde en el commit de release.
- [ ] `server.json`, `directory-profile.json`, ambos README y `CHANGELOG.md` describen la misma versión.
- [ ] Se revisaron disponibilidad, límites de tasa, WAF, alertas y soporte operativo.
- [ ] Se acepta que la metadata ya publicada es inmutable para esa versión; una emergencia se
  atiende con `mcp-publisher status --status deprecated` o `--status deleted`, según corresponda.

Nunca publicar contraseñas demo, tokens OAuth, variables de producción, claves privadas o secretos
del proveedor. Ningún directorio necesita una API key de PropFácil.

## 1. Congelar y validar la release

1. Elegir la versión. Para el primer lanzamiento preparado actualmente: `1.3.8` / `v1.3.8`.
2. Si hubo cambios de producto, actualizar primero el backend y desplegarlo; después actualizar
   `server.json`, el perfil, los README y el changelog.
3. Confirmar que el árbol de trabajo está limpio y que `main` contiene el commit aprobado.
4. Ejecutar localmente las mismas validaciones del workflow:

   ```sh
   jq -e . server.json directory-profile.json .mcp.json
   curl --fail-with-body --silent --show-error \
     -X POST https://registry.modelcontextprotocol.io/v0.1/validate \
     -H 'content-type: application/json' \
     --data-binary @server.json | jq .
   ```

5. Revisar el último workflow remoto:

   ```sh
   gh run list --workflow validate.yml --branch main --limit 5
   ```

Guardar commit, versión, deployment ID y responsable en el registro al final de este documento.

## 2. Publicar en el Official MCP Registry

El workflow `.github/workflows/publish-registry.yml` usa GitHub OIDC, por lo que no requiere un
token del Registry. El permiso `id-token: write` ya está declarado y el namespace coincide con el
usuario de GitHub.

Con el go/no-go aprobado:

```sh
git tag -a v1.3.8 -m "PropFácil MCP 1.3.8"
git push origin v1.3.8
```

El tag activa el workflow, valida que `v1.3.8` coincida con `server.json`, valida el documento ante
el Registry, obtiene identidad GitHub por OIDC y publica la metadata. No ejecutar manualmente el
workflow antes del lanzamiento: `workflow_dispatch` también publica.

Comprobar el resultado:

```sh
gh run list --workflow publish-registry.yml --limit 5
curl --fail --silent --show-error \
  'https://registry.modelcontextprotocol.io/v0.1/servers?search=io.github.jonatanvazquez%2Fpropfacil' \
  | jq .
```

- [ ] El workflow terminó en `success`.
- [ ] La API contiene `io.github.jonatanvazquez/propfacil` versión `1.3.8`.
- [ ] La URL remota es exactamente `https://www.propfacil.com/api/mcp`.
- [ ] Iconos, repositorio y website abren correctamente desde el registro publicado.

Cada actualización posterior debe usar un valor de versión nuevo. No reutilizar una versión para
corregir metadata: las versiones publicadas son inmutables.

## 3. Publicar por URL en Smithery

Ruta recomendada:

1. Entrar a `https://smithery.ai/new` con la cuenta propietaria del namespace.
2. Introducir `https://www.propfacil.com/api/mcp`.
3. Usar el nombre `jonatan/propfacil` dentro del namespace propietario.
4. Permitir el escaneo del contenido público. Si solicita autenticación para completar la parte
   protegida, vincular una cuenta de revisión sin compartir su contraseña públicamente.
5. Si el escáner no puede completar la detección, usar la server card pública
   `https://www.propfacil.com/.well-known/mcp/server-card.json`.
6. Revisar que Smithery describa el endpoint como Streamable HTTP, muestre doce herramientas para el
   modelo más una privada para restauración y distinga acceso público de OAuth.

Alternativa por CLI:

```sh
smithery auth login
smithery mcp publish 'https://www.propfacil.com/api/mcp' \
  -n jonatan/propfacil
```

Si el escaneo devuelve `403`, revisar WAF/bot protection. Un flujo que requiere OAuth debe iniciar
el descubrimiento con `401`, no con `403`; no desactivar controles globales sin evaluar el riesgo.

## 4. Solicitar inclusión en Cline Marketplace

El proceso vigente pide crear un issue en `cline/mcp-marketplace` con:

- Repositorio: `https://github.com/jonatanvazquez/propfacil-mcp`.
- Logo PNG 400×400: `assets/propfacil-icon-400.png`.
- Razón de inclusión basada en `directory-profile.json`.
- Confirmación de que Cline pudo configurarlo leyendo `README.md` o `llms-install.md`.

Antes de crear el issue, probar en Cline una conexión remota con Streamable HTTP. Validar una
búsqueda pública y, si esa versión de Cline soporta OAuth MCP remoto, una operación de favoritos.
Si el host todavía no soporta el OAuth requerido, declararlo de forma transparente: las cuatro
herramientas públicas siguen siendo utilizables y las protegidas requieren un cliente compatible.

- [ ] Se probó la instalación guiada sólo con el contenido público del repositorio.
- [ ] El issue no contiene credenciales, tokens ni enlaces internos.
- [ ] Se guardó la URL del issue y el estado de revisión.

## 5. Directorios agregadores

Después de la publicación oficial, buscar el nombre y endpoint en cada directorio antes de crear un
duplicado. Sus formularios y políticas cambian con frecuencia; confirmar el flujo vigente el día del
lanzamiento.

### Glama

Esperar la ingestión del Official MCP Registry, buscar PropFácil y reclamar el perfil si aparece.
Glama declara que replica todo el Registry oficial. Para un conector alojado como PropFácil, su
pipeline se conecta al endpoint Streamable HTTP; no enviar este repositorio de metadata como si
fuera el código compilable del backend.

### MCP.so

El formulario actual de **Remote Server** pide el endpoint y el nombre. La publicación inmediata es
de pago: **USD 39** al 20 de agosto de 2026. No pagar ni enviar sin autorización expresa. Valores:

- Remote endpoint URL: `https://www.propfacil.com/api/mcp`.
- Name: `PropFácil`.

### PulseMCP

Las altas y cambios manuales están temporalmente pausados. PulseMCP recomienda publicar primero en
el Official MCP Registry y afirma que lo ingerirá automáticamente; no hay un formulario accionable
por ahora.

En todos los casos comprobar nombre, descripción, auth, endpoint, enlaces legales, icono y versión
después de que el listing sea visible.

## 6. Orden sugerido y seguimiento

1. Producción y validación de GitHub.
2. Official MCP Registry.
3. Smithery.
4. Cline Marketplace.
5. Glama, MCP.so y PulseMCP, evitando duplicados ya ingeridos.
6. Añadir a los README los enlaces públicos definitivos cuando cada listing exista.

Durante las primeras 72 horas vigilar:

- Disponibilidad y latencia de `/api/mcp`.
- Errores de `initialize`, `tools/list` y ejecución de tools.
- Fallos de descubrimiento OAuth, DCR, authorization code, refresh y scopes.
- Rechazos anómalos del WAF, abuso y rate limits.
- Enlaces rotos, versión incorrecta o metadata duplicada en los directorios.

Si el problema está sólo en un directorio, corregir su listing sin alterar producción. Si afecta al
servidor, restaurar la última versión estable, documentar el incidente y publicar metadata nueva sólo
cuando corresponda. El Registry no reemplaza la metadata de una versión publicada; para una emergencia,
cambiar el estado de esa release a `deprecated` o `deleted` con el publisher autenticado.

## Releases posteriores

Para cada cambio público:

1. Desplegar y probar el backend.
2. Aumentar la versión en `server.json` y actualizar documentación/changelog.
3. Ejecutar el go/no-go completo.
4. Crear un tag nuevo que coincida exactamente con la versión.
5. Verificar el Registry y actualizar los demás directorios si no ingieren el cambio.

## Registro de lanzamiento

| Campo | Valor |
|---|---|
| Responsable | Apphive / PropFácil |
| Versión/tag | `1.3.8` / [`v1.3.8`](https://github.com/jonatanvazquez/propfacil-mcp/releases/tag/v1.3.8) |
| Commit del repositorio público | `5eb889822b8467e942cb44fdf207f9831eb55f94` |
| Commit/deployment del backend | `c9941a0` desplegado y verificado en producción |
| Official MCP Registry | `1.3.8` activo desde 2026-08-20; workflow OIDC exitoso |
| Smithery | [`jonatan/propfacil`](https://smithery.ai/servers/jonatan/propfacil) publicado el 2026-08-20; release `7b8b1ab1-9e5c-4e4e-b427-73177694baa4` aceptado |
| Cline Marketplace | Prueba real con Cline CLI 3.0.55 completada; [issue #2287](https://github.com/cline/mcp-marketplace/issues/2287) abierto |
| Glama | Espera ingestión automática del Registry y posterior claim |
| MCP.so | Datos enviados al checkout; pago Stripe de USD 39 pendiente de método de pago |
| PulseMCP | Altas manuales pausadas; espera ingestión automática del Registry |

Los valores reutilizables para cada formulario están en
[`directory-profile.json`](../directory-profile.json) y el detalle específico por catálogo en
[`directory-submissions.md`](directory-submissions.md).
