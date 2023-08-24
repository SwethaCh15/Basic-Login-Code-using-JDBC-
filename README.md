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

2.PRODUCT CODE DISPLAYING THE BILL AND UPDATING THE TABLE

package assignment;
import java.util.*;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.sql.*;
public class exam2 
{
	public static void main(String[] args) 
	{
		Scanner sc=new Scanner(System.in);
		Connection con;
		int price=0;
		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
			FileInputStream fi=new FileInputStream("C:\\Users\\KIRAN SOLANKI\\Desktop\\Advance_Java\\Jdbc_First\\src\\assignment\\easy.properties");
			Properties p1=new Properties();
			p1.load(fi);
			con=DriverManager.getConnection("jdbc:mysql://localhost:3306/jdbc_5", p1);
			Statement st=con.createStatement();
			ResultSet rs=st.executeQuery("select * from product");
			System.out.println("the total details of product table:");
			while(rs.next())
			{
				int id=rs.getInt(1);
				String pd=rs.getString(2);
				int pr=rs.getInt(3);
				int quantity=rs.getInt(4);
				System.out.println(id+"\t"+pd+"\t"+pr+"\t"+quantity);
			}
				System.out.println("what product do you wanna buy");
				String pd=sc.next();
				System.out.println("Enter the quantity");
				int item=sc.nextInt();
				if(pd.equalsIgnoreCase("soap"))
				{	
					price=30*item;
					ResultSet r1=st.executeQuery("select quantity from product where pid=1");
					int newquan=0;
					if(r1.next())
					{
						newquan=r1.getInt(1);
					}
					int i=newquan-item;
					st.execute("update product set quantity="+i+" where pid=1");;
				}
				else if(pd.equalsIgnoreCase("shampoo"))
				{
					price=100*item;
					ResultSet r1=st.executeQuery("select quantity from product where pid=2");
					int newquan=0;
					if(r1.next())
					{
						newquan=r1.getInt(1);
					}
					int i=newquan-item;
					st.execute("update product set quantity="+i+" where pid=2");
				}
				else if(pd.equalsIgnoreCase("facewash"))
				{
					price=150*item;
					ResultSet r1=st.executeQuery("select quantity from product where pid=3");
					int newquan=0;
					if(r1.next())
					{
						newquan=r1.getInt(1);
					}
					int i=newquan-item;
					st.execute("update product set quantity="+i+" where pid=3");;
				}
				System.out.println("the total bill of the customer is "+price);
		} catch (ClassNotFoundException | SQLException | IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
}

3.MAX AND MIN PURCHASES OF CUSTOMER , MAX AND MIN USE OF APPLICATION

package assignment;
import java.util.*;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.sql.*;
public class exam3 
{
	public static void main(String[] args) 
	{
		Scanner sc=new Scanner(System.in);
		Connection con;
		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
			FileInputStream fi=new FileInputStream("C:\\Users\\KIRAN SOLANKI\\Desktop\\Advance_Java\\Jdbc_First\\src\\assignment\\easy.properties");
			Properties p1=new Properties();
			p1.load(fi);
			con=DriverManager.getConnection("jdbc:mysql://localhost:3306/jdbc_5", p1);
			Statement st=con.createStatement();
			ResultSet rs=st.executeQuery("select max(purchase) from customer");
			int max_p=0;
			if(rs.next())
			{
				max_p=rs.getInt(1);
			}
			System.out.println("max purchase of customer is "+max_p);
			rs=st.executeQuery("select min(purchase) from customer where purchase!=0");
			int min_p=0;
			if(rs.next())
			{
				min_p=rs.getInt(1);
			}
			System.out.println("min purchase of customer is "+min_p);
			rs=st.executeQuery("select max(used) from app");
			int max_a=0;
			if(rs.next())
			{
				max_a=rs.getInt(1);
			}
			System.out.println("max usage of app is "+max_a);
			rs=st.executeQuery("select min(used) from app where used!=0");
			int min_a=0;
			if(rs.next())
			{
				min_a=rs.getInt(1);
			}
			System.out.println("min usage of app is "+min_a);
			con.close();
		} catch (ClassNotFoundException | IOException | SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
}
