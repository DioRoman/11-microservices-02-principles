# Use official lightweight Python 3.10 image
FROM python:3.10-slim

# Устанавливаем рабочую директорию
WORKDIR /app

# Копируем файл зависимостей в контейнер
COPY requirements.txt .

# Устанавливаем зависимости с фиксированными версиями
RUN pip install --no-cache-dir -r requirements.txt

# Копируем весь код приложения
COPY src ./

# Команда запуска приложения
CMD ["python", "./server.py"]
