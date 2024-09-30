
# شرح طريقة تثبيت Docker و Docker Compose على سيرفر Ubuntu واستخدامهم

## المتطلبات الأساسية:
1. **Ubuntu Server** - يجب أن يكون لديك سيرفر Ubuntu مثبت وجاهز للعمل.
2. **صلاحيات المستخدم** - تحتاج إلى الوصول إلى حساب root أو مستخدم مع صلاحيات sudo.

---

## 1. تثبيت Docker

### الخطوة 1: تحديث الحزم
ابدأ بتحديث قائمة الحزم في نظام Ubuntu للتأكد من أن النظام يعمل بأحدث الإصدارات.

```bash
sudo apt update
sudo apt upgrade
```

### الخطوة 2: تثبيت المتطلبات المبدئية
ستحتاج إلى بعض الأدوات الأساسية التي تساعد في إضافة مستودعات Docker.

```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

### الخطوة 3: إضافة مفتاح GPG الخاص بـ Docker
سنقوم بإضافة المفتاح العام لتأكيد أن الحزم تأتي من مصدر موثوق.

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

### الخطوة 4: إضافة مستودع Docker
الآن سنضيف مستودع Docker الرسمي إلى النظام.

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### الخطوة 5: تثبيت Docker
بعد إضافة المستودع، قم بتثبيت Docker.

```bash
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
```

### الخطوة 6: التحقق من تثبيت Docker
للتحقق من أن Docker قد تم تثبيته بنجاح، استخدم الأمر التالي:

```bash
sudo docker --version
```

---

## 2. تثبيت Docker Compose

### الخطوة 1: تحميل Docker Compose
لتثبيت أحدث إصدار من Docker Compose، يمكنك استخدام الأمر التالي:

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep '"tag_name"' | sed -E 's/.*"([^"]+)".*/\1/')/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

### الخطوة 2: إعطاء الصلاحيات التنفيذية
امنح الأداة صلاحيات التشغيل:

```bash
sudo chmod +x /usr/local/bin/docker-compose
```

### الخطوة 3: التحقق من تثبيت Docker Compose
للتحقق من أن Docker Compose تم تثبيته بنجاح، استخدم الأمر التالي:

```bash
docker-compose --version
```

---

## 3. استخدام Docker

### عرض قائمة الصور (Docker Images):
لعرض قائمة الصور المثبتة على النظام:

```bash
sudo docker images
```

### سحب صورة جديدة (Pulling an Image):
إذا كنت ترغب في تحميل صورة جديدة، مثل صورة Nginx:

```bash
sudo docker pull nginx
```

### تشغيل حاوية (Container):
لتشغيل حاوية (مثال: تشغيل Nginx):

```bash
sudo docker run -d -p 80:80 --name mynginx nginx
```
- `-d`: تشغيل الحاوية في الخلفية.
- `-p 80:80`: ربط المنفذ 80 من الحاوية مع المنفذ 80 من النظام.
- `--name mynginx`: تعيين اسم للحاوية.

### عرض الحاويات العاملة:
لعرض جميع الحاويات العاملة:

```bash
sudo docker ps
```

### عرض جميع الحاويات (حتى المغلقة):
لعرض جميع الحاويات سواء كانت عاملة أو موقفة:

```bash
sudo docker ps -a
```

### عرض السجلات (Logs) الخاصة بحاوية:
لعرض السجلات لحاوية معينة (مثال: `mynginx`):

```bash
sudo docker logs mynginx
```

### إيقاف حاوية:
لإيقاف حاوية عاملة:

```bash
sudo docker stop mynginx
```

### تشغيل حاوية موقفة:
لتشغيل حاوية موقفة:

```bash
sudo docker start mynginx
```

### إزالة حاوية:
لإزالة حاوية موقفة:

```bash
sudo docker rm mynginx
```

### إزالة صورة:
لإزالة صورة:

```bash
sudo docker rmi nginx
```

---

## 4. استخدام Docker Compose

### إنشاء ملف `docker-compose.yml`
أنشئ ملفًا باسم `docker-compose.yml` يحتوي على تعريفات للخدمات التي ترغب في تشغيلها. مثال على تشغيل Nginx و MySQL:

```yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "80:80"
  db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: example
```

### تشغيل الخدمات باستخدام Docker Compose:
لتشغيل الخدمات المعرفة في ملف `docker-compose.yml`:

```bash
sudo docker-compose up -d
```

### إيقاف الخدمات:
لإيقاف الخدمات التي تم تشغيلها:

```bash
sudo docker-compose down
```

---

### الخاتمة
بذلك، تكون قد تعلمت كيفية تثبيت Docker و Docker Compose على Ubuntu، وكيفية التعامل مع الحاويات والصور، بالإضافة إلى عرض السجلات، وإيقاف وتشغيل الحاويات والخدمات.
