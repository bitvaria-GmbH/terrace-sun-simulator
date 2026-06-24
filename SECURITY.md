# Security Policy

## Reporting a vulnerability

Please **do not open a public issue** for security problems.

Report privately via GitHub's [private vulnerability
reporting](https://github.com/bitvaria-GmbH/terrace-sun-simulator/security/advisories/new),
or email **security@bitvaria.com**. We'll acknowledge within a few business days.

## Scope

This is a fully client-side static site with no backend, no authentication, and
no server-side data handling. All computation runs in the visitor's browser;
configuration is stored only in the visitor's own `localStorage` and encoded into
shareable URLs. There is no external network request at runtime — Three.js, the
fonts, and all textures are vendored.

Realistic concerns are therefore limited to client-side issues — for example a
DOM-based XSS vector via the scene-encoding URL parameters, or a vulnerability in
the vendored Three.js (r160). Reports in those areas are appreciated.
