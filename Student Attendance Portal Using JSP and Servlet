----Database Setup----
CREATE DATABASE SchoolDB;
USE SchoolDB;

CREATE TABLE Attendance (
    StudentID INT,
    Date DATE,
    Status VARCHAR(10)
);

----attendance.jsp----
<!DOCTYPE html>
<html>
<head>
    <title>Student Attendance</title>
</head>
<body>
    <h2>Mark Attendance</h2>
    <form action="AttendanceServlet" method="post">
        Student ID: <input type="text" name="studentId" required><br><br>
        Date: <input type="date" name="date" required><br><br>
        Status:
        <select name="status">
            <option value="Present">Present</option>
            <option value="Absent">Absent</option>
        </select><br><br>
        <input type="submit" value="Submit Attendance">
    </form>
</body>
</html>

----AttendanceServlet.java----
import java.io.*;
import java.sql.*;
import jakarta.servlet.*;
import jakarta.servlet.http.*;

public class AttendanceServlet extends HttpServlet {
    private static final String URL = "jdbc:mysql://localhost:3306/SchoolDB";
    private static final String USER = "root";
    private static final String PASSWORD = "root";

    protected void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();

        String studentId = request.getParameter("studentId");
        String date = request.getParameter("date");
        String status = request.getParameter("status");

        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
            Connection con = DriverManager.getConnection(URL, USER, PASSWORD);

            PreparedStatement ps = con.prepareStatement("INSERT INTO Attendance VALUES (?, ?, ?)");
            ps.setInt(1, Integer.parseInt(studentId));
            ps.setString(2, date);
            ps.setString(3, status);
            ps.executeUpdate();

            out.println("<h3>Attendance saved successfully for Student ID: " + studentId + "</h3>");
            out.println("<a href='attendance.jsp'>Go Back</a>");

            con.close();
        } catch (Exception e) {
            out.println("<p>Error: " + e.getMessage() + "</p>");
        }
    }
}

----web.xml----
<servlet>
    <servlet-name>AttendanceServlet</servlet-name>
    <servlet-class>AttendanceServlet</servlet-class>
</servlet>

<servlet-mapping>
    <servlet-name>AttendanceServlet</servlet-name>
    <url-pattern>/AttendanceServlet</url-pattern>
</servlet-mapping>
