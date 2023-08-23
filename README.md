## SchoolDB Veritabanı Projesi
Bu script, **SchoolDB** adlı bir SQL veritabanı oluşturur. Bu veritabanı, bir okulun öğrencileri, öğretmenleri, dersleri, sınavları, devamsızlıkları ve diğer ilişkili bilgilerini içeren verileri depolar.

## School Veritabanı Diyagramı

![School Database Diagram](SchoolDB.png)

## Tablolar ve Değişken Açıklamaları

### Lessons
Bu tablo, okuldaki dersleri temsil eder.
- **Id**: Benzersiz ders kimliği.
- **Name**: Ders adı.
- **TeacherId**: Dersi öğreten öğretmenin kimliği.

### Teachers
Bu tablo, okuldaki öğretmenleri temsil eder.
- **Id**: Benzersiz öğretmen kimliği.
- **IdentityNumber**: Öğretmenin kimlik numarası.
- **NameLastName**: Öğretmenin adı ve soyadı.
- **Gender**: Öğretmenin cinsiyeti.
- **PhoneNumber**: Öğretmenin telefon numarası.
- **AddressId**: Öğretmenin adres bilgilerinin bulunduğu tablo ile ilişkili kimlik.
- **StudentId**: Öğretmenin, danışman öğretmeni olduğu öğrenci kimliği.

### Exams
Bu tablo, okuldaki sınavları temsil eder.
- **Id**: Benzersiz sınav kimliği.
- **LessonsId**: Sınavın yapıldığı dersin kimliği.
- **ExamDate**: Sınav tarihi ve saati.
- **StudentId**: Sınavı alan öğrencinin kimliği.
- **TeacherId**: Sınavı düzenleyen öğretmenin kimliği.

### Students
Bu tablo, okuldaki öğrencileri temsil eder.
- **Id**: Benzersiz öğrenci kimliği.
- **IdentityNumber**: Öğrencinin kimlik numarası.
- **NameLastName**: Öğrencinin adı ve soyadı.
- **Gender**: Öğrencinin cinsiyeti.
- **AddressId**: Öğrencinin adres bilgilerinin bulunduğu tablo ile ilişkili kimlik.
- **ClassId**: Öğrencinin sınıf kimliği.

### Addresses
Bu tablo, adres bilgilerini temsil eder.
- **Id**: Benzersiz adres kimliği.
- **Street**: Cadde/sokak adı.
- **City**: Şehir adı.
- **Country**: Ülke adı.
- **ZipCode**: Posta kodu.
- **AdditionalInfo**: Ekstra adres bilgisi.

### Attendances
Bu tablo, öğrenci devamsızlıklarını temsil eder.
- **Id**: Benzersiz devamsızlık kimliği.
- **StudentId**: Devamsızlık kaydının ait olduğu öğrencinin kimliği.
- **LessonId**: Devamsızlık kaydının ait olduğu dersin kimliği.
- **AttendanceDate**: Devamsızlık tarihi.
- **Status**: Devamsızlık durumu (örneğin: "Geldi", "Gelmedi").

### Classes
Bu tablo, okuldaki sınıfları temsil eder.
- **Id**: Benzersiz sınıf kimliği.
- **Name**: Sınıf adı.

### Notes
Bu tablo, öğrenci notlarını temsil eder.
- **Id**: Benzersiz not kimliği.
- **ExamId**: Notun ait olduğu sınavın kimliği.
- **LessonId**: Notun ait olduğu dersin kimliği.
- **StudentId**: Notun ait olduğu öğrencinin kimliği.
- **Value**: Öğrencinin aldığı not değeri.

### Parents
Bu tablo, öğrenci velilerini temsil eder.
- **Id**: Benzersiz veli kimliği.
- **IdentityNumber**: Veli kimlik numarası.
- **NameLastName**: Veli adı ve soyadı.
- **PhoneNumber**: Veli telefon numarası.
- **AddressId**: Veli adres bilgilerinin bulunduğu tablo ile ilişkili kimlik.
- **StudentId**: Veliye ait öğrenci kimliği.

### Schools
Bu tablo, okulları temsil eder.
- **Id**: Benzersiz okul kimliği.
- **Name**: Okul adı.
- **AddressId**: Okul adres bilgilerinin bulunduğu tablo ile ilişkili kimlik.

### StudentStatuses
Bu tablo, öğrenci not durumlarını temsil eder.
- **Id**: Benzersiz durum kimliği.
- **StudentId**: Not durumunun ait olduğu öğrencinin kimliği.
- **LessonId**: Not durumunun ait olduğu dersin kimliği.
- **GradeAverage**: Öğrencinin not ortalaması.
- **GradeStatus**: Öğrencinin not durumu ("Geçti" veya "Kaldı").

### TeacherSchedules
Bu tablo, öğretmen programlarını temsil eder.
- **Id**: Benzersiz program kimliği.
- **TeacherId**: Programın ait olduğu öğretmenin kimliği.
- **LessonId**: Programın ait olduğu dersin kimliği.
- **DayOfWeek**: Programın yapıldığı haftanın günü.
- **StartTime**: Programın başlangıç saati.
- **EndTime**: Programın bitiş saati.

## İlişkiler

- Lessons tablosu, Teachers tablosu ile TeacherId alanı üzerinden ilişkilendirilmiştir.
- Teachers tablosu, Students tablosu ile StudentId alanı üzerinden ilişkilendirilmiştir.
- Exams tablosu, Lessons, Students ve Teachers tabloları ile ilgili alanlar üzerinden ilişkilendirilmiştir.
- Students tablosu, Addresses ve Classes tabloları ile ilgili alanlar üzerinden ilişkilendirilmiştir.
- Attendances tablosu, Students ve Lessons tabloları ile ilgili alanlar üzerinden ilişkilendirilmiştir.
- Notes tablosu, Exams, Lessons ve Students tabloları ile ilgili alanlar üzerinden ilişkilendirilmiştir.
- Parents tablosu, Addresses ve Students tabloları ile ilgili alanlar üzerinden ilişkilendirilmiştir.

## Prosedürler

1. **GetStudentGrades(studentId INT)**:
   Bu procedure, verilen öğrenci kimliğine göre öğrencinin aldığı notları ve derslerini döndürür.
2. **GetTeacherSchedule(teacherId INT, dayOfWeek INT)**:
   Bu procedure, verilen öğretmen kimliği ve haftanın gününe göre öğretmenin programını döndürür.
3. **GetAbsentStudents(lessonId INT, startDate DATE, endDate DATE)**:
   Bu procedure, belirtilen ders için verilen tarih aralığında devamsızlık yapan öğrencileri döndürür.

## Görünümler

1. **StudentGradesView**:
   Bu view, öğrenci notlarını öğrenci adı-soyadı, ders adı ve not değeri olarak birleştirerek sunar.
2. **TeacherSchedulesView**:
   Bu view, öğretmen programlarını öğretmen adı-soyadı, ders adı, gün ve saat olarak birleştirerek sunar.

## Kurulum

1. Veritabanını oluşturmak için script dosyasını SQL Server Management Studio veya benzeri bir araçla çalıştırın.
2. Projeyi yerel makinenizde veya sunucunuzda çalıştırın.
3. Veritabanına erişim kodları ve bağlantı detayları eklemeyi unutmayın.
