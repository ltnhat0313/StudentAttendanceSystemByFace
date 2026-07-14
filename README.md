# He thong diem danh sinh vien bang nhan dien khuon mat

Day la ung dung su dung cong nghe nhan dien khuon mat thoi gian thuc de xac dinh su hien dien cua sinh vien trong cac lop hoc. He thong su dung Django, OpenCV, FaceNet, SVM va Anti-spoofing de phat hien va nhan dien khuon mat hop le.

## Cong nghe su dung

- Ngon ngu lap trinh: Python
- Framework Web: Django
- Thu vien AI: OpenCV, TensorFlow, PyTorch, Scikit-learn

## Huong dan chay ung dung cuc bo (Local)

Luu y: Du an hien tai da duoc cau hinh lai de su dung co so du lieu SQLite (file db.sqlite3) cuc bo giup chay lap tuc ma khong can cai dat MySQL Server.

### Buoc 1: Cai dat cac thu vien Python
Mo terminal trong thu muc du an va chay lenh sau de cai dat toan bo cac thu vien can thiet:

```bash
.\venv\Scripts\pip.exe install -r requirements_v3.10.txt
```

### Buoc 2: Dong bo co so du lieu (Database Migration)
Tao cau truc cac bang co so du lieu can thiet trong file db.sqlite3 bang cach chay lenh:

```bash
.\venv\Scripts\python.exe manage.py migrate
```

### Buoc 3: Nap du lieu mau (Database Seeding)
Nap toan bo du lieu hoc tap thuc te gom vai tro, giang vien, sinh vien, lop hoc va danh sach lop hoc tu thu muc Database bang cach chay lan luot cac lenh theo dung thu tu duoi day:

```bash
.\venv\Scripts\python.exe manage.py loaddata Database/Role.json
.\venv\Scripts\python.exe manage.py loaddata Database/StaffInfo.json
.\venv\Scripts\python.exe manage.py loaddata Database/StaffRole.json
.\venv\Scripts\python.exe manage.py loaddata Database/StudentInfo.json
.\venv\Scripts\python.exe manage.py loaddata Database/Classroom.json
.\venv\Scripts\python.exe manage.py loaddata Database/StudentClassDetails.json
.\venv\Scripts\python.exe manage.py loaddata Database/BlogPost.json
```

### Buoc 4: Dat lai mat khau cho tai khoan Admin
Mat khau cua cac tai khoan trong file du lieu mau da duoc ma hoa. De dat mat khau cho tai khoan quan tri cao nhat (admin) ve mat khau moi, hay chay lenh:

```bash
"from main.models import StaffInfo; from django.contrib.auth.hashers import make_password; admin_user = StaffInfo.objects.get(id_staff='admin'); admin_user.password = make_password('admin123'); admin_user.save(); print('Successfully changed admin password')" | .\venv\Scripts\python.exe manage.py shell
```

Luu y: Cac tai khoan Giag vien va Sinh vien con lai deu da duoc tu dong dat mat khau mac dinh la "123456" de de dang dang nhap thu nghiem.

### Buoc 5: Khoi dong may chu phat trien (Run Server)
Chay lenh sau de khoi dong website:

```bash
.\venv\Scripts\python.exe manage.py runserver
```

Truy cap vao duong dan tren trinh duyet web: http://127.0.0.1:8000/

## Thong tin tai khoan dang nhap thu nghiem

1. Tai khoan Admin (Quan tri vien):
- Tên dang nhap: admin
- Mat khau: admin123
- Link truy cap: http://127.0.0.1:8000/login

2. Tai khoan Giang vien (Lecturer):
- Ten dang nhap (ID): 2013497810
- Mat khau: 123456
- Link truy cap: http://127.0.0.1:8000/login

3. Tai khoan Sinh vien (Student):
- Ten dang nhap (ID): 2011003929
- Mat khau: 123456
- Link truy cap: http://127.0.0.1:8000/student/login

## Cac luu y quan trong khi su dung cac chuc nang AI
- Chuc nang diem danh bang khuon mat va chup anh khuon mat sinh vien se truy cap vao Webcam mac dinh (chi so index 0) cua may tinh. Hay dam bao webcam dang hoat dong binh thuong.
- Cac mo hinh AI cua he thong nhu FaceNet, SVM va MiniFASNet hien da duoc dat day du trong thu muc main/Models va main/resources va duoc load tu dong khi khoi chay.
