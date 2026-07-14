# He thong diem danh sinh vien bang nhan dien khuon mat

Day la ung dung su dung cong nghe nhan dien khuon mat thoi gian thuc de xac dinh su hien dien cua sinh vien trong cac lop hoc. He thong su dung Django, OpenCV, FaceNet, SVM va Anti-spoofing de phat hien va nhan dien khuon mat.

Moi truong chay de xuat: Python 3.10 (vi du: Python 3.10.1).

---

## Huong dan cai dat va chay ung dung tu dau (Step-by-Step)

Du an da duoc cau hinh mac dinh su dung co so du lieu SQLite (file db.sqlite3 se tu dong sinh ra khi dong bo), vi vay khong can cai dat MySQL Server.

### Buoc 1: Mo Terminal/Command Prompt
Mo terminal (Command Prompt hoac PowerShell tren Windows, Terminal tren macOS/Linux) tai thu muc goc cua du an.

### Buoc 2: Tao moi truong ao Python (Virtual Environment)
Chay lenh duoi day de tao thu muc moi truong ao ten la venv:

```bash
python -m venv venv
```

### Buoc 3: Kich hoat moi truong ao
Tuy thuoc vao he dieu hanh va loai terminal ban dang su dung, chay mot trong cac lenh sau de kich hoat:

- Tren Windows (PowerShell):
  ```bash
  .\venv\Scripts\Activate.ps1
  ```
- Tren Windows (Command Prompt - CMD):
  ```bash
  .\venv\Scripts\activate.bat
  ```
- Tren macOS/Linux (Terminal):
  ```bash
  source venv/bin/activate
  ```

Sau khi kich hoat thanh cong, ban se thay ky tu (venv) xuat hien o dau dong lenh cua terminal.

### Buoc 4: Cai dat cac thu vien (Dependencies)
Chay lenh sau de tai va cai dat cac thu vien can thiet tu file requirements:

```bash
pip install -r requirements_v3.10.txt
```

Luu y: Qua trinh nay se tai cac thu vien lon nhu TensorFlow, PyTorch va OpenCV nen se mat tu 5 den 10 phut tuy vao toc do internet cua ban.

### Buoc 5: Dong bo va khoi tao co so du lieu (Database Migration)
Chay lenh sau de Django tu dong tao file db.sqlite3 va tao cau truc bang du lieu:

```bash
python manage.py migrate
```

### Buoc 6: Nap du lieu mau vao co so du lieu (Seeding Data)
Chay lan luot cac lenh duoi day theo dung thu tu de nap thong tin lop hoc, giang vien, sinh vien va bai viet vao co so du lieu (khong chay sai thu tu de tranh loi khoa ngoai):

```bash
python manage.py loaddata Database/Role.json
python manage.py loaddata Database/StaffInfo.json
python manage.py loaddata Database/StaffRole.json
python manage.py loaddata Database/StudentInfo.json
python manage.py loaddata Database/Classroom.json
python manage.py loaddata Database/StudentClassDetails.json
python manage.py loaddata Database/BlogPost.json
```

### Buoc 7: Khoi tao mat khau cho tai khoan Admin
Mat khau cua cac tai khoan trong file du lieu mau da duoc ma hoa. De dat mat khau cho tai khoan quan tri cao nhat (admin) ve mat khau moi, hay chay lenh:

```bash
python manage.py shell
```

Khi shell interactive cua python hien ra (ky hieu >>>), copy toan bo doan code duoi day, dan vao va an Enter:

```python
from main.models import StaffInfo
from django.contrib.auth.hashers import make_password
admin_user = StaffInfo.objects.get(id_staff="admin")
admin_user.password = make_password("admin123")
admin_user.save()
print("Success")
exit()
```

Luu y: Tat ca cac tai khoan Giang vien va Sinh vien con lai deu da duoc tu dong thiet lap mat khau mac dinh la "123456" de ban tien dang nhap test he thong.

### Buoc 8: Chay server phat trien (Run Server)
Khoi dong may chu de truy cap vao ung dung web:

```bash
python manage.py runserver
```

Sau khi chay lenh, mo trinh duyet web va truy cap duong dan: http://127.0.0.1:8000/

---

## Thong tin tai khoan test cac phan he

1. Phan he Admin (Quan tri vien):
- Ten dang nhap: admin
- Mat khau: admin123
- Link dang nhap: http://127.0.0.1:8000/login

2. Phan he Giang vien (Lecturer):
- Ten dang nhap (ID): 2013497810
- Mat khau: 123456
- Link dang nhap: http://127.0.0.1:8000/login

3. Phan he Sinh vien (Student):
- Ten dang nhap (ID): 2011003929
- Mat khau: 123456
- Link dang nhap: http://127.0.0.1:8000/student/login

---

## Luu y khi su dung chuc nang AI
- Chuc nang diem danh bang khuon mat (Giang vien) va chup anh dang ky guong mat (Admin) yeu cau may tinh phai co Webcam/Camera dang hoat dong binh thuong. He thong mac dinh goi camera so 0 (webcam chinh).
- Cac mo hinh AI cua he thong (FaceNet, SVM va MiniFASNet) da duoc luu day du trong thu muc main/Models va main/resources va se tu dong load khi chay chuong trinh.
