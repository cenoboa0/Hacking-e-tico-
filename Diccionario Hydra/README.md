# wordlist_ctf — Diccionario para laboratorios de ciberseguridad

Diccionario curado para prácticas de pentesting en entornos controlados (CTF, laboratorios educativos). **No debe usarse contra sistemas sin autorización explícita.**

## Contenido

| Categoría | Entradas aprox. | Descripción |
|---|---|---|
| Gestores de contraseñas | ~250 | KeePass, LastPass, Bitwarden y variantes |
| Contraseñas comunes | ~600 | Top passwords de listas educativas públicas |
| Base + sufijos numéricos | ~4,000 | `admin1`…`admin99`, `password1`…`password99` |
| Patrones P@ssword | ~200 | Sustituciones leetspeak + símbolos |
| Meses y temporadas + año | ~400 | `Summer2024`, `January2023!`, etc. |
| Variantes capitalizadas | resto | Formas upper/capitalize de todas las anteriores |

**Total: 9,000 entradas únicas** — diseñado para ~3 minutos de escaneo con Hydra a velocidad típica HTTP (~50 req/s).

## Uso con Hydra

```bash
# HTTP GET form
hydra -l admin -P wordlist_ctf.txt TARGET http-get-form \
  "/ruta/login.php:user=^USER^&pass=^PASS^:F=Incorrect"

# HTTP POST form
hydra -l admin -P wordlist_ctf.txt TARGET http-post-form \
  "/ruta/login.php:user=^USER^&pass=^PASS^:F=Incorrect"

# Con más hilos (más rápido, más ruidoso)
hydra -l admin -P wordlist_ctf.txt -t 16 TARGET http-get-form \
  "/ruta/login.php:user=^USER^&pass=^PASS^:F=Incorrect"
```

## Filosofía del diccionario

Este diccionario no es fuerza bruta exhaustiva. Aplica **inteligencia contextual**:

1. **Prioridad a gestores de contraseñas** al inicio del archivo — si la pista del reto menciona gestores, la contraseña correcta aparece en los primeros segundos.
2. **Patrones reales** basados en comportamiento humano documentado (meses, años, sustituciones comunes).
3. **Espacio reducido intencionalmente** — 52^8 combinaciones son inviables; 9,000 candidatos bien elegidos son prácticos.

> La lección de fondo: cuando la fuerza bruta pura es computacionalmente inviable, el vector más eficiente es **inteligencia contextual** (OSINT, pistas del sistema, ingeniería social) en lugar de cobertura exhaustiva del espacio de claves.

## Estimaciones de tiempo

| Velocidad Hydra | Tiempo estimado |
|---|---|
| 30 req/s (red lenta / protecciones) | ~5 minutos |
| 50 req/s (HTTP local/lab típico) | ~3 minutos |
| 100 req/s (con `-t 16` y sin throttle) | ~1.5 minutos |

## Aviso legal

Este material es exclusivamente para:
- Entornos CTF (Capture The Flag)
- Laboratorios propios o con autorización escrita
- Formación académica en ciberseguridad

El uso contra sistemas sin autorización explícita es ilegal. El autor no se responsabiliza del mal uso de este recurso.

## Fuentes de referencia

- Subset educativo de SecLists (danielmiessler/SecLists)
- Patrones documentados en estudios de contraseñas filtradas (Have I Been Pwned análisis)
- Variantes comunes observadas en CTFs públicos (HackTheBox, TryHackMe, PicoCTF)
