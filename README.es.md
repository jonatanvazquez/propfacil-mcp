<!-- mcp-name: io.github.jonatanvazquez/propfacil -->

<p align="center">
  <img src="assets/propfacil-icon-512.png" width="144" height="144" alt="PropFácil">
</p>

# PropFácil MCP

Servidor remoto Model Context Protocol para encontrar inventario inmobiliario autorizado en México.
La búsqueda, las fichas y el contacto disponible son públicos; favoritos, listas y publicación usan OAuth.

> [Read in English](README.md)

## Conexión

- **Endpoint MCP:** `https://www.propfacil.com/api/mcp`
- **Transporte:** Streamable HTTP
- **Versión actual:** `1.3.1`
- **Server card:** `https://www.propfacil.com/.well-known/mcp/server-card.json`
- **Documentación:** `https://www.propfacil.com/docs`

```json
{
  "mcpServers": {
    "propfacil": {
      "type": "http",
      "url": "https://www.propfacil.com/api/mcp"
    }
  }
}
```

Es un servidor alojado: no se clona este repositorio para ejecutarlo y no se necesita una API key.
Los clientes compatibles inician automáticamente OAuth al usar una herramienta protegida.

Consulta la [guía de instalación](docs/installation.md), la [referencia de herramientas](docs/tools.md)
y los [detalles de autenticación](docs/authentication.md).

## Capacidades

| Capacidad | Acceso |
|---|---|
| Buscar propiedades por ciudad, precio, recámaras, operación o radio | Público |
| Consultar una ficha | Público |
| Obtener contacto y enlaces autorizados de una propiedad concreta | Público |
| Mostrar tarjetas, comparación y mapa en hosts compatibles con MCP Apps | Público |
| Consultar y administrar listas de favoritos | OAuth |
| Consultar publicaciones propias y publicar | OAuth |

Todos los clientes MCP con Streamable HTTP pueden consumir las herramientas y resultados estructurados.
Las interfaces enriquecidas requieren soporte para MCP Apps UI y las operaciones de cuenta requieren OAuth MCP.

## Alcance del repositorio

Este repositorio contiene solamente metadata pública de distribución, documentación y recursos de marca.
El backend de producción se mantiene por separado.

- Metadata del Official MCP Registry: [`server.json`](server.json)
- Configuración genérica: [`.mcp.json`](.mcp.json)
- Instrucciones para agentes: [`llms-install.md`](llms-install.md)
- Perfil reutilizable para directorios: [`directory-profile.json`](directory-profile.json)
- Runbook de lanzamiento: [`docs/launch-runbook.md`](docs/launch-runbook.md)
- Notas por directorio: [`docs/directory-submissions.md`](docs/directory-submissions.md)

## Políticas y soporte

- [Privacidad](https://www.propfacil.com/privacidad)
- [Términos](https://www.propfacil.com/terminos)
- [Soporte](https://www.propfacil.com/soporte)
- [Seguridad](SECURITY.md)

La documentación y los ejemplos se distribuyen bajo la [licencia MIT](LICENSE). El nombre y logotipo
PropFácil no forman parte de esa licencia; consulta [TRADEMARKS.md](TRADEMARKS.md).
