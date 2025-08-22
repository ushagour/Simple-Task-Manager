
زيان بزاف 👌 غادي نديرولك واحد **roadmap مشروع Fullstack (Node + React + Mongo)** ونربطوه مع **Docker, Docker Compose, Travis CI** باش تستعمل داكشي اللي بغيتي فالحقيقي.

---

## 🏗️ الفكرة ديال المشروع

مثال: **"Simple Task Manager"**

* **Frontend (React):** UI باش المستخدم يضيف/يحذف/يعدل تاسكات.
* **Backend (Node + Express):** API RESTful.
* **Database (MongoDB):** تخزين التاسكات.

---

## 🧩 البنية ديال المشروع

```
project/
│── backend/        # Node + Express API
│   ├── Dockerfile
│   └── ...
│
│── frontend/       # React app
│   ├── Dockerfile
│   └── ...
│
│── docker-compose.yml
│── .travis.yml
```

---

## 🐳 Dockerfiles

### 1. Backend (`backend/Dockerfile`)

```dockerfile
FROM node:18

WORKDIR /app
COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 5000
CMD ["npm", "start"]
```

---

### 2. Frontend (`frontend/Dockerfile`)

```dockerfile
FROM node:18

WORKDIR /app
COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000
CMD ["npm", "start"]
```

---

## 🐙 docker-compose.yml

باش تربط **frontend + backend + MongoDB** مع بعضهم:

```yaml
version: "3"
services:
  backend:
    build: ./backend
    ports:
      - "5000:5000"
    depends_on:
      - mongo
    environment:
      - MONGO_URI=mongodb://mongo:27017/tasksdb

  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
    depends_on:
      - backend

  mongo:
    image: mongo:6
    ports:
      - "27017:27017"
    volumes:
      - mongo-data:/data/db

volumes:
  mongo-data:
```

---

## ⚡ Travis CI (.travis.yml)

باش كل push يتبنى أو يتست:

```yaml
sudo: required

services:
  - docker

script:
  # Build backend
  - docker build -t myapp/backend ./backend
  # Build frontend
  - docker build -t myapp/frontend ./frontend
  # Run tests (optional)
  # - docker run myapp/backend npm test
  # - docker run myapp/frontend npm test
```

---

## 🚀 Workflow ديالك

1. تكتب الكود (React + Node + Mongo).
2. تدير **docker-compose up** باش يطلع المشروع كامل locally.
3. تدير **push** للكود → Travis كيخدم:

   * يبني Docker images.
   * يقدر حتى يدفعهم لـ **Docker Hub** (إلا زدنا auth).

---

👨‍💻 هاد الطريقة كتوري أنك كتتحكم فـ:

* **Fullstack dev** (React, Node, Mongo).
* **Containerization** (Docker).
* **Orchestration** (Docker Compose).
* **CI/CD** (Travis CI).

---

تحب نزيدك كيفاش تـ **push Docker images تلقائياً لـ Docker Hub** عبر Travis (باش تولي عندك pipeline كامل)؟ 🚀
زيان بزاف 👌 غادي نديرولك واحد **roadmap مشروع Fullstack (Node + React + Mongo)** ونربطوه مع **Docker, Docker Compose, Travis CI** باش تستعمل داكشي اللي بغيتي فالحقيقي.

---

## 🏗️ الفكرة ديال المشروع

مثال: **"Simple Task Manager"**

* **Frontend (React):** UI باش المستخدم يضيف/يحذف/يعدل تاسكات.
* **Backend (Node + Express):** API RESTful.
* **Database (MongoDB):** تخزين التاسكات.

---

## 🧩 البنية ديال المشروع

```
project/
│── backend/        # Node + Express API
│   ├── Dockerfile
│   └── ...
│
│── frontend/       # React app
│   ├── Dockerfile
│   └── ...
│
│── docker-compose.yml
│── .travis.yml
```

---

## 🐳 Dockerfiles

### 1. Backend (`backend/Dockerfile`)

```dockerfile
FROM node:18

WORKDIR /app
COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 5000
CMD ["npm", "start"]
```

---

### 2. Frontend (`frontend/Dockerfile`)

```dockerfile
FROM node:18

WORKDIR /app
COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000
CMD ["npm", "start"]
```

---

## 🐙 docker-compose.yml

باش تربط **frontend + backend + MongoDB** مع بعضهم:

```yaml
version: "3"
services:
  backend:
    build: ./backend
    ports:
      - "5000:5000"
    depends_on:
      - mongo
    environment:
      - MONGO_URI=mongodb://mongo:27017/tasksdb

  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
    depends_on:
      - backend

  mongo:
    image: mongo:6
    ports:
      - "27017:27017"
    volumes:
      - mongo-data:/data/db

volumes:
  mongo-data:
```

---

## ⚡ Travis CI (.travis.yml)

باش كل push يتبنى أو يتست:

```yaml
sudo: required

services:
  - docker

script:
  # Build backend
  - docker build -t myapp/backend ./backend
  # Build frontend
  - docker build -t myapp/frontend ./frontend
  # Run tests (optional)
  # - docker run myapp/backend npm test
  # - docker run myapp/frontend npm test
```

---

## 🚀 Workflow ديالك

1. تكتب الكود (React + Node + Mongo).
2. تدير **docker-compose up** باش يطلع المشروع كامل locally.
3. تدير **push** للكود → Travis كيخدم:

   * يبني Docker images.
   * يقدر حتى يدفعهم لـ **Docker Hub** (إلا زدنا auth).

---

👨‍💻 هاد الطريقة كتوري أنك كتتحكم فـ:

* **Fullstack dev** (React, Node, Mongo).
* **Containerization** (Docker).
* **Orchestration** (Docker Compose).
* **CI/CD** (Travis CI).

---

تحب نزيدك كيفاش تـ **push Docker images تلقائياً لـ Docker Hub** عبر Travis (باش تولي عندك pipeline كامل)؟ 🚀
