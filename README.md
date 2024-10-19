import javax.swing.*;
import javax.swing.table.DefaultTableModel;
import java.awt.*;
import java.util.Vector;

public class CarServiceAppointmentApp extends JFrame {
    private JTextField nameField;
    private JTextField modelField;
    private JTextField dateField;
    private JTextField serviceField;
    private JTextField insuranceField;
    private JTextField emailField;
    private JTextField phoneField;
    private JTextField addressField;
    private JTable table;
    private DefaultTableModel tableModel;

    public CarServiceAppointmentApp() {
        setTitle("Car Service Appointment");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setSize(700, 500);
        setLocationRelativeTo(null);


        nameField = new JTextField(15);
        modelField = new JTextField(15);
        dateField = new JTextField(15);
        serviceField = new JTextField(15);
        insuranceField = new JTextField(15);
        emailField = new JTextField(15);
        phoneField = new JTextField(15);
        addressField = new JTextField(15);


        JButton addButton = new JButton("Add Appointment");
        addButton.addActionListener(e -> addAppointment());


        JButton receiptButton = new JButton("Generate Receipt");
        receiptButton.addActionListener(e -> generateReceipt());


        tableModel = new DefaultTableModel(new String[]{
                "ID", "Customer Name", "Car Model", "Appointment Date", "Service Type", "Insurance Number", "Email", "Phone", "Address"}, 0);
        table = new JTable(tableModel);
        table.setFillsViewportHeight(true);


        JPanel inputPanel = new JPanel(new GridBagLayout());
        GridBagConstraints gbc = new GridBagConstraints();
        gbc.insets = new Insets(5, 5, 5, 5);


        gbc.gridx = 0; gbc.gridy = 0;
        inputPanel.add(new JLabel("Name:"), gbc);
        gbc.gridx = 1; gbc.gridy = 0;
        inputPanel.add(nameField, gbc);

        gbc.gridx = 0; gbc.gridy = 1;
        inputPanel.add(new JLabel("Car Model:"), gbc);
        gbc.gridx = 1; gbc.gridy = 1;
        inputPanel.add(modelField, gbc);

        gbc.gridx = 0; gbc.gridy = 2;
        inputPanel.add(new JLabel("Date:"), gbc);
        gbc.gridx = 1; gbc.gridy = 2;
        inputPanel.add(dateField, gbc);

        gbc.gridx = 0; gbc.gridy = 3;
        inputPanel.add(new JLabel("Service Type:"), gbc);
        gbc.gridx = 1; gbc.gridy = 3;
        inputPanel.add(serviceField, gbc);

        gbc.gridx = 0; gbc.gridy = 4;
        inputPanel.add(new JLabel("Insurance No:"), gbc);
        gbc.gridx = 1; gbc.gridy = 4;
        inputPanel.add(insuranceField, gbc);

        gbc.gridx = 0; gbc.gridy = 5;
        inputPanel.add(new JLabel("Email:"), gbc);
        gbc.gridx = 1; gbc.gridy = 5;
        inputPanel.add(emailField, gbc);

        gbc.gridx = 0; gbc.gridy = 6;
        inputPanel.add(new JLabel("Phone:"), gbc);
        gbc.gridx = 1; gbc.gridy = 6;
        inputPanel.add(phoneField, gbc);

        gbc.gridx = 0; gbc.gridy = 7;
        inputPanel.add(new JLabel("Address:"), gbc);
        gbc.gridx = 1; gbc.gridy = 7;
        inputPanel.add(addressField, gbc);

        gbc.gridx = 0; gbc.gridy = 8;
        inputPanel.add(addButton, gbc);
        gbc.gridx = 1; gbc.gridy = 8;
        inputPanel.add(receiptButton, gbc);


        add(inputPanel, BorderLayout.WEST);
        add(new JScrollPane(table), BorderLayout.CENTER);
    }

    private void addAppointment() {

        Vector<String> row = new Vector<>();
        row.add(String.valueOf(tableModel.getRowCount() + 1)); // ID
        row.add(nameField.getText());
        row.add(modelField.getText());
        row.add(dateField.getText());
        row.add(serviceField.getText());
        row.add(insuranceField.getText());
        row.add(emailField.getText());
        row.add(phoneField.getText());
        row.add(addressField.getText());

        tableModel.addRow(row);
        clearFields();
        JOptionPane.showMessageDialog(this, "Appointment added successfully!");
    }

    private void clearFields() {
        nameField.setText("");
        modelField.setText("");
        dateField.setText("");
        serviceField.setText("");
        insuranceField.setText("");
        emailField.setText("");
        phoneField.setText("");
        addressField.setText("");
    }

    private void generateReceipt() {
        int selectedRow = table.getSelectedRow();
        if (selectedRow == -1) {
            JOptionPane.showMessageDialog(this, "Please select an appointment to generate a receipt.");
            return;
        }


        String customerName = (String) tableModel.getValueAt(selectedRow, 1);
        String carModel = (String) tableModel.getValueAt(selectedRow, 2);
        String appointmentDate = (String) tableModel.getValueAt(selectedRow, 3);
        String serviceType = (String) tableModel.getValueAt(selectedRow, 4);
        String insuranceNumber = (String) tableModel.getValueAt(selectedRow, 5);
        String email = (String) tableModel.getValueAt(selectedRow, 6);
        String phone = (String) tableModel.getValueAt(selectedRow, 7);
        String address = (String) tableModel.getValueAt(selectedRow, 8);


        String receipt = "----- Receipt -----\n" +
                "Customer Name: " + customerName + "\n" +
                "Car Model: " + carModel + "\n" +
                "Appointment Date: " + appointmentDate + "\n" +
                "Service Type: " + serviceType + "\n" +
                "Insurance Number: " + insuranceNumber + "\n" +
                "Email: " + email + "\n" +
                "Phone: " + phone + "\n" +
                "Address: " + address + "\n" +
                "-------------------";


        JOptionPane.showMessageDialog(this, receipt, "Receipt", JOptionPane.INFORMATION_MESSAGE);
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            CarServiceAppointmentApp app = new CarServiceAppointmentApp();
            app.setVisible(true);
        });
    }
}
