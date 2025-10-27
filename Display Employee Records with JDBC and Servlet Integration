----Database Setup----
CREATE DATABASE CompanyDB;
USE CompanyDB;

CREATE TABLE Employee (
    EmpID INT PRIMARY KEY,
    Name VARCHAR(50),
    Salary DOUBLE
);

INSERT INTO Employee VALUES (1, 'Vishal', 50000);
INSERT INTO Employee VALUES (2, 'Ankit', 60000);
INSERT INTO Employee VALUES (3, 'Neha', 70000);


------EmployeeServlet.java----
import java.io.*;
import java.sql.*;
import jakarta.servlet.*;
import jakarta.servlet.http.*;

public class EmployeeServlet extends HttpServlet {
    private static final String URL = "jdbc:mysql://localhost:3306/CompanyDB";
    private static final String USER = "root";
    private static final String PASSWORD = "root"; // change if needed

    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();

        String empId = request.getParameter("empId");
        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
            Connection con = DriverManager.getConnection(URL, USER, PASSWORD);
            Statement st = con.createStatement();

            String query;
            if (empId != null && !empId.isEmpty()) {
                query = "SELECT * FROM Employee WHERE EmpID=" + empId;
            } else {
                query = "SELECT * FROM Employee";
            }

            ResultSet rs = st.executeQuery(query);
            out.println("<h2>Employee Records</h2>");
            out.println("<form action='EmployeeServlet' method='get'>"
                      + "Search by ID: <input type='text' name='empId'>"
                      + "<input type='submit' value='Search'></form><br>");

            out.println("<table border='1'><tr><th>ID</th><th>Name</th><th>Salary</th></tr>");
            while (rs.next()) {
                out.println("<tr><td>" + rs.getInt("EmpID") + "</td>"
                        + "<td>" + rs.getString("Name") + "</td>"
                        + "<td>" + rs.getDouble("Salary") + "</td></tr>");
            }
            out.println("</table>");

            con.close();
        } catch (Exception e) {
            out.println("<p>Error: " + e.getMessage() + "</p>");
        }
    }
}


------web.xml----
<servlet>
    <servlet-name>EmployeeServlet</servlet-name>
    <servlet-class>EmployeeServlet</servlet-class>
</servlet>

<servlet-mapping>
    <servlet-name>EmployeeServlet</servlet-name>
    <url-pattern>/EmployeeServlet</url-pattern>
</servlet-mapping>
