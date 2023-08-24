# Basic-Login-Code-using-JDBC-
1. BASIC LOGIN CODE

package assignment;
import java.util.*;

import com.mysql.cj.protocol.Resultset;

import java.sql.*;
public class exam1 {
	public static void main(String[] args) {
		Scanner sc=new Scanner(System.in);
		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
			String url="jdbc:mysql://localhost:3306/jdbc_5";
			String user="root";
			String pswrd="root";
			Connection con=DriverManager.getConnection(url,user,pswrd);
			Statement st=con.createStatement();
			System.out.println("enter the username");
			String user_name=sc.next();
			ResultSet rs=st.executeQuery("select user from credentials");
			while(rs.next())
			{
				String data_user=rs.getString(1);
				if(user_name.equalsIgnoreCase(data_user))
				{
					System.out.println("Enter the password");
					String ps=sc.next();
					ResultSet r1=st.executeQuery("select password from credentials");
					while(r1.next())
					{
						String uswr_ps=r1.getString(1);
						if(ps.equalsIgnoreCase(uswr_ps))
						{
							System.out.println("Login Successful");
							break;
						}
						else
						{
							System.out.println("incorrect password");
							break;
						}
					}
				}
				else 
				{
					System.out.println("incorrect username");
					break;
				}
			}
			con.close();
		} catch (ClassNotFoundException | SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
}

 
 
			  
					   
			 
 
		 
			 
			 
