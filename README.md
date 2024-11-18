# StudentPerformanceAnalysis
 A Java Swing application for student performance analysis
String name =txtname.getText();
String age =txtmobile.getText();
String course =txtcourse.getText();

      try {
          Class.forName("com.mysql.jdbc.Driver"); //Register the mysql driver
          con1 = DriverManager.getConnection("jdbc:mysql://localhost/linda","root","");
          insert = con1.prepareStatement("insert into record (name,mobile,course)values(?,?,?)");
          insert.setString(1,name);
          insert.setString(2,age);
          insert.setString(3,course);
          insert.executeUpdate();
          JOptionPane.showMessageDialog(this, "Record Saved");
          
          
          txtname.setText("");
          txtmobile.setText("");
          txtcourse.setText("");
          table_update();

      } catch (ClassNotFoundException ex) {
          Logger.getLogger(crud.class.getName()).log(Level.SEVERE, null, ex);
      } catch (SQLException ex) {
          Logger.getLogger(crud.class.getName()).log(Level.SEVERE, null, ex);
      }   private void table_update() {
        int CC;
        try {
            Class.forName("com.mysql.jdbc.Driver");
            con1 = DriverManager.getConnection("jdbc:mysql://localhost/linda","root","");
            insert = con1.prepareStatement("SELECT * FROM record");
            ResultSet Rs = insert.executeQuery();
            
            ResultSetMetaData RSMD = Rs.getMetaData();
            CC = RSMD.getColumnCount();
            DefaultTableModel DFT = (DefaultTableModel) jTable1.getModel();
            DFT.setRowCount(0);

            while (Rs.next()) {
                Vector v2 = new Vector();
           
                for (int ii = 1; ii <= CC; ii++) {
                    v2.add(Rs.getString("id"));
                    v2.add(Rs.getString("name"));
                    v2.add(Rs.getString("mobile"));
                    v2.add(Rs.getString("course"));
                }
                DFT.addRow(v2);
            }
        } catch (Exception e) {
        }
    }public crud() 
     {
        initComponents();
        table_update();  // when the form is loaded all the records will be shown on the jTable.
     }DefaultTableModel model = (DefaultTableModel) jTable1.getModel();
int selectedIndex = jTable1.getSelectedRow();
      
txtname.setText(model.getValueAt(selectedIndex, 1).toString());
txtmobile.setText(model.getValueAt(selectedIndex, 2).toString());
txtcourse.setText(model.getValueAt(selectedIndex, 3).toString());    DefaultTableModel model = (DefaultTableModel) jTable1.getModel();
    int selectedIndex = jTable1.getSelectedRow();
    try {   
        
    int id = Integer.parseInt(model.getValueAt(selectedIndex, 0).toString());
    String name =txtname.getText();
    String mobile =txtmobile.getText();
    String course =txtcourse.getText();
  
    Class.forName("com.mysql.jdbc.Driver");
    con1 = DriverManager.getConnection("jdbc:mysql://localhost/linda","root","");
    insert = con1.prepareStatement("update record set name= ?,mobile= ?,course= ? where id= ?");
    insert.setString(1,name);
    insert.setString(2,mobile);
    insert.setString(3,course);
    insert.setInt(4,id);
    insert.executeUpdate();
    JOptionPane.showMessageDialog(this, "Record Updated");
    txtname.setText("");
    txtmobile.setText("");
    txtcourse.setText("");
    table_update();
   
    
} catch (ClassNotFoundException ex) {
   
} catch (SQLException ex) {
          DefaultTableModel model = (DefaultTableModel) jTable1.getModel();
          int selectedIndex = jTable1.getSelectedRow();
            try {   
                
            int id = Integer.parseInt(model.getValueAt(selectedIndex, 0).toString());
            int dialogResult = JOptionPane.showConfirmDialog (null, "Do you want to Delete the               record","Warning",JOptionPane.YES_NO_OPTION);
            if(dialogResult == JOptionPane.YES_OPTION){

            Class.forName("com.mysql.jdbc.Driver");
            con1 = DriverManager.getConnection("jdbc:mysql://localhost/linda","root","");
            insert = con1.prepareStatement("delete from record where id = ?");
        
            insert.setInt(1,id);
            insert.executeUpdate();
            JOptionPane.showMessageDialog(this, "Record Delete");
            txtname.setText("");
            txtmobile.setText("");
            txtcourse.setText("");

            table_update();
           
           }

        } catch (ClassNotFoundException ex) {
        
        } catch (SQLException ex) {
            
        }
}   
