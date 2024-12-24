# Python Pathlib Kutubxonasi Bo'yicha To'liq Darslik

**Kirish**

Python dasturlash tilida fayl va kataloglar bilan ishlash ko'pincha zarur bo'lib turadi. An'anaviy usullarga qaraganda, `pathlib` kutubxonasi ob'ektga yo'naltirilgan yondashuvni taklif etadi, bu esa kodni o'qish va yozishni osonlashtiradi. Ushbu darslikda `pathlib` kutubxonasining barcha asosiy metodlari va ularning misollari bilan tanishasiz.

**Reja**

1. [Pathlib Kutubxonasi Kirish](#pathlib-kutubxonasi-kirish)
2. [Path Ob'ekti Yaratish](#path-objekti-yaratish)
3. [Fayl va Katalog Mavjudligini Tekshirish](#fayl-va-katalog-mavjudligini-tekshirish)
4. [Fayl va Katalog Turi](#fayl-va-katalog-turi)
5. [Katalog Yaratish va O'chirish](#katalog-yaratish-va-o'chirish)
6. [Fayl Yaratish, O'qish va Yozish](#fayl-yaratish-oqish-va-yozish)
7. [Path Ob'ekti Bo'yicha Navigatsiya](#path-objekti-bo'yicha-navigatsiya)
8. [Fayllarni Qayta Nomlash va O'chirish](#fayllarni-qayta-nomlash-va-ochirish)
9. [Pathlib bilan Qidiruv](#pathlib-bilan-qidiruv)
10. [Qo'shimcha Metodlar va Xususiyatlar](#qo'shimcha-metodlar-va-xususiyatlar)
11. [Xulosa](#xulosa)

---

## Pathlib Kutubxonasi Kirish

`pathlib` Python 3.4 versiyasidan boshlab standart kutubxonaga kiritilgan bo'lib, fayl tizimlari bilan ishlashni soddalashtiradi. Bu kutubxona yordamida fayl va katalog yo'llarini ob'ekt sifatida ifodalash, ularni boshqarish va ularga bog'liq operatsiyalarni amalga oshirish mumkin.

```python
from pathlib import Path
```

## Path Ob'ekti Yaratish

Path ob'ekti yaratish uchun `Path` klassidan foydalaniladi. Bu klass operatsion tizimga mos keladigan yo'lni avtomatik ravishda tanlaydi.

```python
from pathlib import Path

# Joriy ish katalogini olish
current_path = Path.cwd()
print(current_path)

# Uy katalogini olish
home_path = Path.home()
print(home_path)

# Aniq yo'l yaratish
specific_path = Path("/home/user/Documents")
print(specific_path)
```

## Fayl va Katalog Mavjudligini Tekshirish

`exists()`, `is_file()`, va `is_dir()` metodlari yordamida fayl yoki katalog mavjudligini va turini tekshirish mumkin.

```python
path = Path("example.txt")

# Mavjudligini tekshirish
if path.exists():
    print("Fayl yoki katalog mavjud.")
else:
    print("Mavjud emas.")

# Fayl ekanligini tekshirish
if path.is_file():
    print("Bu fayl.")

# Katalog ekanligini tekshirish
if path.is_dir():
    print("Bu katalog.")
```

## Fayl va Katalog Turi

Path ob'ekti orqali fayl yoki katalog turini aniqlash mumkin.

```python
path = Path("/home/user/Documents/example.txt")

# Fayl turi (extension) ni olish
print(path.suffix)  # .txt

# Fayl nomini olish
print(path.name)  # example.txt

# Fayl nomining asosiy qismini olish
print(path.stem)  # example

# Katalog nomlarini olish
print(path.parent)  # /home/user/Documents
```

## Katalog Yaratish va O'chirish

`mkdir()` va `rmdir()` metodlari yordamida katalog yaratish va o'chirish mumkin.

```python
from pathlib import Path

# Yangi katalog yaratish
new_dir = Path("new_folder")
new_dir.mkdir(exist_ok=True)
print("Katalog yaratildi.")

# Bo'sh katalogni o'chirish
new_dir.rmdir()
print("Katalog o'chirildi.")
```

**Eslatma:** `rmdir()` faqat bo'sh kataloglarni o'chiradi. Agar katalog ichida fayllar bo'lsa, avval ularni o'chirish kerak.

## Fayl Yaratish, O'qish va Yozish

`touch()`, `read_text()`, `write_text()`, `read_bytes()`, va `write_bytes()` metodlari bilan fayllar bilan ishlash mumkin.

```python
from pathlib import Path

file_path = Path("sample.txt")

# Fayl yaratish (agar mavjud bo'lmasa)
file_path.touch()

# Matn yozish
file_path.write_text("Salom, bu Pathlib misoli!")

# Matn o'qish
content = file_path.read_text()
print(content)

# Faylni o'chirish
file_path.unlink()
```

## Path Ob'ekti Bo'yicha Navigatsiya

Path ob'ekti orqali yo'lni kesish, qo'shish va boshqa navigatsiyalarni amalga oshirish mumkin.

```python
from pathlib import Path

path = Path("/home/user/Documents/example.txt")

# Katalog bilan birlashtirish
new_path = path.parent / "new_folder"
print(new_path)  # /home/user/Documents/new_folder

# Qism yo'l olish
print(path.parts)  # ('/', 'home', 'user', 'Documents', 'example.txt')

# Yuqoridagi katalogni olish
print(path.parent)

# Ikki daraja yuqoriga chiqish
print(path.parents[1])
```

## Fayllarni Qayta Nomlash va O'chirish

`rename()` va `replace()` metodlari bilan fayllarni qayta nomlash va harakatlantirish mumkin. `unlink()` metodi faylni o'chirish uchun ishlatiladi.

```python
from pathlib import Path

old_file = Path("old_name.txt")
new_file = Path("new_name.txt")

# Fayl yaratish
old_file.touch()

# Faylni qayta nomlash
old_file.rename(new_file)
print(f"Fayl {old_file} dan {new_file} ga nomlandi.")

# Faylni o'chirish
new_file.unlink()
print("Fayl o'chirildi.")
```

## Pathlib bilan Qidiruv

`glob()` va `rglob()` metodlari bilan fayllarni qidirish mumkin.

```python
from pathlib import Path

# Joriy katalogda barcha .txt fayllarni qidirish
for txt_file in Path(".").glob("*.txt"):
    print(txt_file)

# Katalog va uning ichidagi barcha kataloglarda .py fayllarni qidirish
for py_file in Path(".").rglob("*.py"):
    print(py_file)
```

## Qo'shimcha Metodlar va Xususiyatlar

`pathlib` ko'plab qo'shimcha metodlar va xususiyatlarga ega:

- `resolve()`: Absolyut yo'lni olish.
- `absolute()`: Absolyut yo'lni olish (ba'zi holatlarda `resolve()` bilan farq qiladi).
- `with_name(name)`: Fayl nomini almashtirish.
- `with_suffix(suffix)`: Fayl kengaytmasini almashtirish.
- `iterdir()`: Katalogdagi barcha elementlarni iteratsiya qilish.

### Misollar

```python
from pathlib import Path

path = Path("example.txt")

# Absolyut yo'lni olish
absolute_path = path.resolve()
print(absolute_path)

# Fayl nomini almashtirish
new_name_path = path.with_name("new_example.txt")
print(new_name_path)

# Katalog ichidagi barcha elementlarni ko'rish
for item in Path(".").iterdir():
    print(item)
```

## Xulosa

`pathlib` Python dasturchilariga fayl va kataloglar bilan ishlashni soddalashtiradi. Ob'ektga yo'naltirilgan yondashuv kodni yanada o'qilishi va boshqarilishini osonlashtiradi. Ushbu darslikda `pathlib` kutubxonasining asosiy metodlari va ularning qo'llanilishi bilan tanishdingiz. Amaliyotda qo'llash orqali bu kutubxonaning qulayliklaridan to'liq foydalana olasiz.
