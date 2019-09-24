# furry-succotash
package com.briup;

import java.io.*;
import java.sql.*;

public class Tupian {
    public static void main(String[] args) throws IOException, ClassNotFoundException, SQLException {
//        new Tupian().uploading();
        new Tupian().downloading();
    }

    public void uploading() throws ClassNotFoundException, SQLException, IOException {
        Class.forName("com.mysql.jdbc.Driver");
        Connection conn = DriverManager.getConnection("jdbc:mysql://192.168.112.136:3306/briup", "root", "root");
        String sql = "insert into tupian1 values(?,?)";
        PreparedStatement sts = conn.prepareStatement(sql);
        FileInputStream bis = new FileInputStream("src\\com\\briup\\2.png");
        sts.setInt(1, 2);
        sts.setBinaryStream(2, bis);
        sts.execute();
        bis.close();
        sts.close();
        conn.close();
    }

    public void downloading() throws ClassNotFoundException, SQLException, IOException {
        Class.forName("com.mysql.jdbc.Driver");
        Connection conn = DriverManager.getConnection("jdbc:mysql://192.168.112.136:3306/briup", "root", "root");
        String sql = "select * from tupian1";
        Statement sts = conn.createStatement();
        ResultSet rs = sts.executeQuery(sql);
        FileOutputStream fos = new FileOutputStream("C:\\Users\\Administrator\\Desktop\\dd.png");
        byte[] bytes = new byte[1024 * 1024];
        InputStream cc;
        while (rs.next()) {
            cc = rs.getBinaryStream(2);
            while (cc.read(bytes) != -1) {
                fos.write(bytes);
            }
        }
        fos.close();
        rs.close();
        sts.close();
        conn.close();
    }
}
