# Hệ thống điểm danh danh sinh viên bằng khuôn mặt

Hệ thống điểm danh sinh viên bằng khuôn mặt là một ứng dụng sử dụng công nghệ nhận diện khuôn mặt để xác định sự hiện diện của sinh viên trong các buổi học

## Tech Stack

**Language:** Python

**Framework:** Django

## Run Locally

Install dependencies

- If use python version 3.7

  ```bash
  pip install -r requirements_v3.7.txt
  ```
- If use python version 3.10

  ```bash
  pip install -r requirements_v3.10.txt
  ```

Creating migration files

```bash
  python manage.py makemigrations
```

Applying database migrations

```bash
  python manage.py migrate
```

Start the server

```bash
  python manage.py runserver
```
