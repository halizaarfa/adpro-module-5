# Adpro - Profiling
Haliza N. S. Arfa | 2306211401 | Adpro A

---

## JMeter Report and Test Results
### **Endpoint** `/all-student`

**a) Before Optimization**

GUI Test Result:
![image](https://github.com/user-attachments/assets/de7a37d2-4083-4e1f-87e7-3fc014bf63a2)

Command Line Test Result:
![image](https://github.com/user-attachments/assets/a4a52334-8d93-49fc-9e6d-ed5fff9889f9)

**b) After Optimization**
![image](https://github.com/user-attachments/assets/d76d74f3-3b0d-4680-9989-144f15ecdda8)

Execution Time `getAllStudentWithCourses()` from Intellij Profiler:

| Before | After | Diff Percentage |
| -- | -- | -- |
| 17,542 ms | 1,466 ms | 91.65% |


### **Endpoint** `/all-student-name`

**a) Before Optimization**

GUI Test Result:
![image](https://github.com/user-attachments/assets/0c741dd9-2ec3-49ab-8703-d1f3ab4f3618)

Command Line Test Result:
![image](https://github.com/user-attachments/assets/6ff7a8a6-16cb-477c-b73a-bc753bc065a9)

**b) After Optimization**
![image](https://github.com/user-attachments/assets/80af6fc8-2059-4420-8a0a-977bab4e4436)

Execution Time `joinStudentNames()` from Intellij Profiler:

| Before | After  | Diff Percentage |
|--------|--------| -- |
| 979 ms | 230 ms | 76.5% |


### **Endpoint** `/highest-gpa`

**a) Before Optimization**

GUI Test Result:
![image](https://github.com/user-attachments/assets/b439d40a-782a-4c66-8c87-7a5f03f98e55)

Command Line Test Result:
![image](https://github.com/user-attachments/assets/cf6c3c02-f0f3-4e32-8d4b-421259da86d8)

**b) After Optimization**
![image](https://github.com/user-attachments/assets/02038e8b-1b72-45c1-87ef-42715adbc427)

Execution Time `findStudentWithHighestGpa()` from Intellij Profiler:

| Before | After | Diff Percentage |
|--------|-------| -- |
| 180 ms | 40 ms | 77.7% |
