# هنا انا بمشي خطوه خطوه بمعنى يعنى المفروض يكون فى جافا 
# بعدين يبقى فى ميفن 
# بعدين اعمل الكود وهكذا كل ده بعمله بالترتيب اكنى بعمل هيكله للمشروع



#  الحاجه اللى هسططبها او اكبر حاجه وليكن جافا 11
# FROM baseImage
FROM openjdk:11


# هنا بعمل مسار لملف عشان احط الحاجات الى عاوزها فيه يعنى ذي مجلد داخل ال الدوكر
# WORKDIR /the/workdir/path
WORKDIR /app


# هنا بجيب الملفات الى عاوز احطها فى الدوكر واخليه يعملها هنا بجيب الفيل والمسار اللى فى الدوكر اللى هحطها فيه
# COPY source dest -----> COPY . .   معناها انقل كل الملفات بتاعت المشروع داخل الدوكر
# COPY source dest

COPY pom.xml .
COPY mvnw .
COPY .mvn .mvn
COPY pom.xml .
COPY src src


# عشان مثلا لو عاوز اعمل حاجه فى حاله معينه 

ARG ENV
RUN if["$ENV" == "dev"]; \ 
    then  mvn install package ; \
    else  mvn install package ; \
    fi

# هنا بقوله شغلى التطبيق بس على حسب الامر الى هكتبه
# RUN command
# RUN mvn -f /home/app/pom.xml clean package -----. مثلا كدا لو هوا فى مسار داخل الدوكر 
# RUN mvn package ------> كدا امر مباشر بدون حوارات
RUN mvn package




# هنا بحط البورت اللى هكلم فيه المشروع من داخل الدوكر 
# EXPOSE port
EXPOSE 4000

# لو عاوز اعمل متغيرات واستخدمها 
ENV PORT=8080
# Expose the ports your application will use
EXPOSE $PORT



# CMD [ "executable" ] ---->  هذا وقت الشغيل بقا بكتب الاوامر الى تتنفذ من بناء وما شابهه
# CMD [ "npm" ,"start" ] ------> مثال عل  ال نود ج اس  






# command docker

 
# هنا بقا هعمل بناء للملف كله بس 
# docker build  (-t  name_image ) ./name_docker_file  or docker build (-t  name_image ) .


# هنا بقا بشوف كل الصور االلى موجوده فى دوكر 
# docker image ls


# هنا بقا عشان اشغل الصوره 
# docker run (--name  name_image_container) (-v path_project : name_layer_in image (:ro) ) (-v name_file) (--env PORT=8080 --env MODE=x ) (--env-file ./.env)  (-d)  (-p 4000:4000) name_image 

# (--name  name_image_container) ------->  هنا بقا بعمل اسم للكونتينر عشان لو هعمل اكتر من واحد على نفس الصوره

# (-v path_project : name_layer_in image )  ----->  دى بعملها عشان لما اغير حاجه مش كل شويه اعمل بناء للدوكر فبعمل هوت ريلود  بخلى االى يتغير هنا يسمع هنا والعكس بدون عمل ريبلد
# (-v path_project : name_layer_in image : ro )  -----> عشان اعمل قراءه فقط انه يغير فى المشروع يسمع فى الدوكر وليس العكس
# $(pwd)--> linux  , %cd% --> windows   print working directory  -------> replace path_project
# (-v name_file) -----> بعمل ده عشان لو عاوز امنع التتغير فى ملف لو عامل  هوت ريلود 

# (--env PORT=8080 --env MODE=x ) دى عشان لو عاوز ابعتله متغيرات او عنده متغيرات فى الملف وانا عاوز اغيرها
# (--env-file ./.env) دى عشان لو عامل ملف فيه كل المتغيرات ابعتها فى ملف افضل من الاوامر

# -d ----> هنا بقا عشان مش يظهر اى معلومات عن الصوره 

# (-p 4000:4000) ------->  هنا بقول له خلى البورت اللى عملته يسمع على الجهاز على بورت 4000 برضو وممكن اغيره عادى



# هنا بيجيب اللى بيحصل والاخطاء 
# docker logs name_image_container




# هنا هعرض اللى شغال بس
# docker ps





# هنا بقا هعمل بناء للملف كله بس 
# docker run (--name  name_image_container) (-d) name_image 



# ده عشان افتح الكونتينر واعدل عليه واعمل اللى عاوزه فيه وهوا على ال دوكر نفسه 
# docker exec -it name_image_container bash 



# ده بعمله عشان مش يحمل كل حاجه معاه عشان اعمل تخطى لبعض الملفات حتى لا ياخذ الجميع
# .dockerignore
# بداخله بحط اسماء الملفات والمجلدات  الى مش عاوزه يضعها فى الاعتبار



# 




## full example
FROM openjdk:11
WORKDIR /app
COPY . .
RUN javac Main.java
CMD ["java", "Main"]






## full example Spring boot

# Use the official Maven image to build the application
FROM maven:3-jdk-11 AS build
WORKDIR /comma

# Copy the Maven project files
COPY pom.xml .
COPY src ./src

# Clean and install the application
RUN mvn clean package
RUN mvn install package
#RUN mvn clean install

# Use the official OpenJDK base image
FROM openjdk:11-jre-slim As runtime

# Set the working directory inside the container
WORKDIR /comma

# Copy the compiled Spring Boot JAR file from the build stage
COPY --from=build /comma/target/E-Commerce-0.0.1-SNAPSHOT.jar app.jar

# Expose the ports your application will use
EXPOSE 8080

# Start the Spring Boot application
CMD ["java", "-jar", "app.jar"]


#docker build -t  comma-care  .
#docker run --name  comma_care_container  -v D:\Working\Mostafa\E-Commerce:/comma -d  -p 8080:8080 comma-care
