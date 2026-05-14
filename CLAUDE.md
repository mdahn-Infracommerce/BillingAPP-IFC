# BillingAPP IFC — Contexto de Proyecto

## Qué es este proyecto
Dashboard web de auditoría de facturación para **Infracommerce**. Valida la consistencia entre facturas de proveedores (Go Personal) y facturas emitidas a clientes (NGR, Hiraoka, Tailoy, Softys).

## Stack
- HTML/CSS/JS puro — un único archivo `index.html` (sin frameworks, sin build step)
- Desplegado en **Vercel** via GitHub
- URL de producción: **https://billing-app-ifc.vercel.app**

## Repositorio
- GitHub: `https://github.com/mdahn-Infracommerce/BillingAPP-IFC`
- Rama principal: `main`
- Remote configurado con SSH: `git@github.com:mdahn-Infracommerce/BillingAPP-IFC.git`

## Deploy key SSH
- Clave privada: `/Users/max/Documents/Claude/Projects/IFC-FC/.ssh/deploy_key`
- Clave pública registrada en GitHub como deploy key con permisos de escritura
- Git ya configurado con `core.sshCommand` apuntando a esa clave

## Cómo hacer push desde el sandbox
```bash
cd /sessions/<session-id>/mnt/IFC-FC
# Detectar el mount path actual:
REPO=$(find /sessions -name "index.html" -path "*/IFC-FC/*" 2>/dev/null | head -1 | xargs dirname)
cd $REPO
GIT_SSH_COMMAND="ssh -i /Users/max/Documents/Claude/Projects/IFC-FC/.ssh/deploy_key -o StrictHostKeyChecking=no -o IdentitiesOnly=yes" git push origin main
```

## Reglas de negocio — Márgenes por marca
| Marca    | Tipo  | Margen       |
|----------|-------|--------------|
| NGR      | Fijo  | 10% sobre costo |
| Hiraoka  | Fijo  | 20% sobre costo |
| Tailoy   | Rango | 15% – 20%    |
| Softys   | Rango | 15% – 20%    |
| Otro     | Rango | 15% – 20%    |

- Margen fuera de rango → estado **"Alerta de Margen"**
- Desfase entre fin de período y recepción de factura > 30 días → advertencia **"Posible impacto en P&L por desfase contable"**

## Archivos del proyecto
```
IFC-FC/
├── index.html       # App completa (login + dashboard + auditoría)
├── vercel.json      # Config de Vercel (security headers, cleanUrls)
├── .gitignore       # Excluye .ssh/ y archivos PDF
├── CLAUDE.md        # Este archivo
└── .ssh/
    ├── deploy_key     # Clave privada SSH (no commitear)
    └── deploy_key.pub # Clave pública SSH
```

## Login de la app
- Usuario: `infracommerce`  
- Contraseña: `IFC2024!`  
- ⚠️ Cambiar en `index.html` → sección `CONFIGURACIÓN` antes de compartir el link

## Datos
Los datos de facturas se persisten en `localStorage` del navegador del usuario. No hay base de datos. Si se requiere persistencia compartida en el futuro, migrar a Supabase o similar.

## Contacto del proyecto
- Organización GitHub: `mdahn-Infracommerce`
- Email: `info@celeritysolutions.ai`
