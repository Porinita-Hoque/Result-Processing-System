# Result Processing System

This SQL project is about Result Processing System, an automated system that will generate and record the result (CGPA) of the students in each semester. Besides the system will  also have a record of the results of a student in each course at each semester along with obtained marks so that he/she can evaluate himself/herself. In addition, this also provides a feature to determine whether a student will be eligible to sit for the exam or not, depending on his/her attendance percentage.

<hr>

### Features
- First of all, the DataBase operator will insert the values into the Student table where the ID & Semester is auto-generated.
- Then the course table is updated according to corresponding courses in each semester. Students in a semester will get those corresponding courses. By doing so, assigning courses to a student will be dynamic.
- Marks for a student (in a particular course once) is then inserted. While inserting each time, the result calculation trigger calls the result calculating function which then and there calculates the grades for that course and keeping the credit in consideration, the grade is stored, later summed up to generate the final result.
- One important criterion for passing is Attendance. Anybody below 75% attendance will not be eligible for the exam. So, by knowing the attendance percentage of a student, we can decide whether he’s going to sit for the exam or not. If not, then going through the calculation process for him/her is useless. So, this feature makes the system more realistic

<hr>

### Details about BackEnd
- Tables
  - Student (ID, Dept, DOA (Date of Admission), Prog, Scheme)
  - Course (ID, Credit, Semester)
  - Marks (Student ID, Course ID, Attendance, Quiz1, Quiz2, Quiz3, Quiz4, Midterm, Final)
  - CGPA (Student ID, Semester, GPA, CGPA)

- Functions
  - Gen_ID – Automated ID generation – From Admission Year, Dept, Program, Roll 
  - Gen_Semester – Automated Semester generation – From Date of Admission
  - InputMarks
    - Takes the ID of a student
    - Inputs the marks for each course of that student
    - Calculates the grade for each course
    - Sums up the grade & Calculates the GPA
  - ReturnAttendance
    - Checks the mark of Attendance
    - Calculates the percentage, if less than 75, Student is not eligible for exam

- Triggers
  - Student_ID_Sem_Generating_Trigger
    - Generates ID & Semester 
    - Each time some data has been inserted to Student table, it works
  - Student_Result_Generating_Trigger
    - Each time marks for a student in a course is inserted, the Trigger call InputMarks function
    - The function calculates the grade of that course and stores temporarily as the current GPA
    - When marks are inserted for all the courses of a semester then the semester’s GPA is calculated
    - Then depending on the semester of the student the CGPA is also updated

- Cursors
  - C_Course
    - Resided into the last-mentioned function
    - Takes input for each course
    - Exits when there’s no course left for a student in a semester
