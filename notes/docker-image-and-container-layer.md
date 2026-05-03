# Docker Layers (Simple Explanation)

## One-Line Idea

> Image = read-only
> Container = read-write layer on top

---

## Step 1: What is an Image?

Example:

```bash
docker pull ubuntu:22.04
```

* This downloads a **ready-made template**
* You **cannot change it**
* It is **read-only**

---

## Step 2: What happens when you run a container?

```bash
docker run -it ubuntu:22.04
```

Docker does this:

```
[ Image (read-only) ]
        +
[ Container layer (read/write) ]
```

-> A new writable layer is added on top

---

## Step 3: What if you create a file?

Inside container:

```bash
touch test.txt
```

Result:

* File is created in **container layer**
* Image remains unchanged

---

## Step 4: What if you delete a file?

```bash
rm /etc/hostname
```

* File is NOT deleted from image
* It is hidden in container layer

👉 This is called **copy-on-write**

---

## Easy Analogy

```
Cake base  → Image (fixed)
Cream top  → Container (changeable)
```

You only change the top, not the base.

---

## Step 5: What happens when container stops?

```bash
docker run --rm ubuntu
```

* Container is deleted
* All changes are lost

! Your file `test.txt` is gone

---

## Final Memory Trick

* Image = base (read-only)
* Container = temporary changes

---