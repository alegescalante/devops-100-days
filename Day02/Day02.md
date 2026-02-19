# Día 2: Usuario Linux Temporal con Fecha de Expiración

## 🎯 Objetivo

Crear un usuario Linux **con fecha de expiración**, ideal para accesos temporales (contratistas, soporte puntual, labs).

---

## 🧠 Contexto

Las cuentas temporales reducen riesgos de seguridad. Definir una fecha de expiración evita que accesos queden activos por olvido.

---

## 🛠️ Paso a paso

### 1️⃣ Conectarse al servidor correcto

Ingresá al servidor indicado por el reto (App Server correspondiente):

```bash
ssh <usuario>@<servidor>
```

Confirmá:

```bash
hostname
```

---

### 2️⃣ Crear el usuario con fecha de expiración

Usá `useradd` con la opción `-e` (formato `YYYY-MM-DD`):

```bash
sudo useradd -m -e 2027-03-28 anita
```

> 📌 `-m` crea el directorio home del usuario.

Si el reto indica otro usuario/fecha (ej. `yousuf`, `2027-02-17`), ajustá el comando:

```bash
sudo useradd -m -e 2027-02-17 yousuf
```

---

### 3️⃣ (Opcional) Asignar contraseña

Solo si el reto lo requiere:

```bash
sudo passwd anita
```

---

### 4️⃣ Verificar que el usuario fue creado

```bash
id anita
```

Salida esperada (ejemplo):

```
uid=1006(anita) gid=1006(anita) groups=1006(anita)
```

---

### 5️⃣ Verificar la fecha de expiración

```bash
sudo chage -l anita
```

Debe verse algo como:

```
Account expires : Mar 28, 2027
```

---

## ❌ Errores comunes

* Crear el usuario en el **servidor incorrecto**
* Usar mal el formato de fecha
* Crear el usuario sin `sudo`
* Nombre con mayúsculas (ej. `Anita`)

---

## ✅ Checklist final

* [x] Usuario creado
* [x] Fecha de expiración configurada
* [x] Verificado con `chage -l`

---

> 📌 **Reto 100 Días de DevOps** – Día 2 completado. Automatización segura habilitada 🔑🚀
>
> ---
>
> # Temporary User Setup with Expiry Date

As part of the temporary assignment to the Nautilus project, a developer named yousuf requires access for a limited duration. To ensure smooth access management, a temporary user account with an expiry date is needed. Here's what you need to do:

> Create a user named `yousuf` on `App Server 1` in Stratos Datacenter. Set the expiry date to `2024-01-28`, ensuring the user is created in lowercase as per standard protocol.

## Steps

1. Follow the [Day 01](./001.md) to connect server and run the following command:

    ```sh
    sudo useradd -m -e 2024-01-28 yousuf
    ```

2. Verify

    ```sh
    cat /etc/passwd
    sudo su yousuf
    ```

## Good to Know?

### User Account Expiry

- **Purpose**: Automatically disable accounts after specified date
- **Format**: YYYY-MM-DD (ISO 8601 standard)
- **Check Expiry**: `chage -l username` shows account aging info
- **Extend Expiry**: `sudo chage -E 2024-12-31 username`

### Temporary Account Management

- **Best Practice**: Always set expiry for temporary accounts
- **Monitoring**: Use `chage -l` to track account status
- **Cleanup**: Expired accounts remain but cannot login
- **Removal**: Use `userdel -r username` to completely remove

### Related Commands

- `chage`: Modify user password expiry information
- `usermod -e`: Modify existing user's expiry date
- `passwd -S`: Check password status
