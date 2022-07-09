import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.ArrayList;

public class Cart extends JFrame {
    String[] beauty={"Flour",
            "Milo","Eggs","Soy Sauce",
            "Nescafe","Dairy Milk Choclate Bar","Milk",
            "Yogurt","Cooking Oil"};

    Double[] beautyPrice={5.40,6.20,13.20,4.50,10.00,6.60,7.20,3.80,12.00};

    ArrayList<ItemInformation> carts = new ArrayList<>();

    Cart(Customer customer,ArrayList<ItemInformation> carts){
        JLabel jlCarts = new JLabel("Your Carts");
        JPanel panelNorth = new JPanel();
        JPanel panelSouth = new JPanel();
        jlCarts.setFont(new Font("MV Boli", Font.BOLD, 25));
        jlCarts.setForeground(Color.BLUE);
        JButton jbtConfirmPayment=new JButton("Make Payment");
        JButton jbtCancel=new JButton("Cancel");
        JPanel panelSubwindow = new JPanel();


        panelNorth.add(jlCarts);

        JLabel id = new JLabel("Item ID");
        JLabel name = new JLabel("Item Name");
        JLabel price = new JLabel("Item Price");
        JLabel qty = new JLabel("Quantity");

        panelSubwindow.add(id);
        panelSubwindow.add(name);
        panelSubwindow.add(price);
        panelSubwindow.add(qty);

        id.setHorizontalAlignment(SwingConstants.CENTER);
        name.setHorizontalAlignment(SwingConstants.CENTER);
        price.setHorizontalAlignment(SwingConstants.CENTER);
        qty.setHorizontalAlignment(SwingConstants.CENTER);

        id.setFont(new Font("Verdana", Font.BOLD, 15));
        name.setFont(new Font("Verdana", Font.BOLD, 15));
        price.setFont(new Font("Verdana", Font.BOLD, 15));
        qty.setFont(new Font("Verdana", Font.BOLD, 15));


        id.setForeground(Color.orange);
        name.setForeground(Color.orange);
        price.setForeground(Color.orange);
        qty.setForeground(Color.orange);

        JLabel jlID, jlName, jlPrice, jlQty;

        for (ItemInformation itemInformation : carts) {
            jlID = new JLabel(itemInformation.getItemId());
            jlName = new JLabel(itemInformation.getItemName());
            jlPrice = new JLabel(String.format("RM%.2f", itemInformation.getItemPrice()));
            jlQty = new JLabel(String.valueOf(itemInformation.getQty()));
            panelSubwindow.add(jlID);
            panelSubwindow.add(jlName);
            panelSubwindow.add(jlPrice);
            panelSubwindow.add(jlQty);
            jlID.setHorizontalAlignment(SwingConstants.CENTER);
            jlName.setHorizontalAlignment(SwingConstants.CENTER);
            jlPrice.setHorizontalAlignment(SwingConstants.CENTER);
            jlQty.setHorizontalAlignment(SwingConstants.CENTER);
        }


        panelSubwindow.setLayout(new GridLayout(carts.size() + 1, 4));
        panelSouth.add(jbtConfirmPayment);
        panelSouth.add(jbtCancel);

        jbtConfirmPayment.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                new PaymentInterface(customer,carts);
            }
        });

        add(panelSouth, BorderLayout.SOUTH);
        add(panelNorth, BorderLayout.NORTH);
        add(panelSubwindow, BorderLayout.CENTER);//Add subwindow to the mainframe and make it visible
        setTitle("Customer Carts");
        setVisible(true);
        pack();
        setLocationRelativeTo(null);
    }
}
public class CustomerInformation {
    String custId;
    String custIC;
    double CounterPaid;

    public CustomerInformation(String custId, String custIC, double counterPaid) {
        this.custId = custId;
        this.custIC = custIC;
        CounterPaid = counterPaid;
    }

    public String getCustId() {
        return custId;
    }

    public void setCustId(String custId) {
        this.custId = custId;
    }

    public String getCustIC() {
        return custIC;
    }

    public void setCustIC(String custIC) {
        this.custIC = custIC;
    }

    public double getCounterPaid() {
        return CounterPaid;
    }

    public void setCounterPaid(double counterPaid) {
        CounterPaid = counterPaid;
    }
}
public class Customer {
    private String name;
    private String email;
    private String phoneNo;

    public String getPhoneNo() {
        return phoneNo;
    }

    public void setPhoneNo(String phoneNo) {
        this.phoneNo = phoneNo;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }


    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public Customer(String name,String email, String phoneNo) {
        this.name = name;
        this.email = email;
        this.phoneNo=phoneNo;
    }
}

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.LinkedList;

public class CustomerLogin extends JFrame  {
    LinkedList<Customer> customerList=new LinkedList<Customer>();
    JLabel customerName = new JLabel("Customer Name");
    JLabel customerPhoneNo = new JLabel("Phone No");
    JLabel email = new JLabel("Email");
    JTextField custNameField = new JTextField(25);
    JTextField custPhoneNoField = new JTextField(25);
    JTextField emailField = new JTextField(25);
    JButton loginButton = new JButton("PURCHASE ORDER");
    JButton resetButton = new JButton("RESET");

    CustomerLogin() {
        JPanel panelNorth = new JPanel();
        JLabel label = new JLabel("~ Welcome To Hypermarket Self-Checkout Automated System ~");
        label.setForeground(Color.red);//set font color of text
        label.setFont(new Font("MV Boli", Font.BOLD, 25));//set font of text
        panelNorth.add(label);
        panelNorth.add(new JLabel(""));
        add(panelNorth, BorderLayout.NORTH);


        JPanel panelCenter = new JPanel(new GridLayout(3, 2));
        panelCenter.add(customerName);
        panelCenter.add(custNameField);
        panelCenter.add(email);
        panelCenter.add(emailField);
        panelCenter.add(customerPhoneNo);
        panelCenter.add(custPhoneNoField);
        add(panelCenter, BorderLayout.CENTER);

        JPanel panelSouth = new JPanel();
        panelSouth.add(loginButton);
        panelSouth.add(resetButton);
        add(panelSouth, BorderLayout.SOUTH);

        setLocationRelativeTo(null);
        setVisible(true);
        pack();
        //setBounds(100,100,450,350);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setTitle("Supermarket Info Center");


        loginButton.addActionListener(new LoginListener());
        resetButton.addActionListener(new ResetListener());


    }

    public class LoginListener implements ActionListener {
        @Override
        public void actionPerformed(ActionEvent e) {
            Customer customer=new Customer(custNameField.getText(),custPhoneNoField.getText(),emailField.getText());
            customerList.add(customer);
            new Menu(customer);
        }
    }

    public class ResetListener implements ActionListener {
        @Override
        public void actionPerformed(ActionEvent e) {
            custNameField.setText("");
            custPhoneNoField.setText("");
            email.setText("");
        }
    }

    public static void main(String[] a) {
        CustomerLogin frame = new CustomerLogin();
    }


}

import java.time.LocalDate;


public class ItemInformation {
    private String itemId;
    private String itemName;
    private Double itemPrice;

    public int getQty() {
        return qty;
    }

    public void setQty(int qty) {
        this.qty = qty;
    }

    private int qty;
    LocalDate datePurchase;

    public String getItemId() {
        return itemId;
    }

    public void setItemId(String itemId) {
        this.itemId = itemId;
    }

    public String getItemName() {
        return itemName;
    }

    public void setItemName(String itemName) {
        this.itemName = itemName;
    }

    public Double getItemPrice() {
        return itemPrice;
    }

    public void setItemPrice(Double itemPrice) {
        this.itemPrice = itemPrice;
    }

    public LocalDate getDatePurchase() {
        return datePurchase;
    }

    public void setDatePurchase(LocalDate datePurchase) {
        this.datePurchase = datePurchase;
    }

    public ItemInformation(String itemId, String itemName,int qty, Double itemPrice, LocalDate datePurchase) {
        this.itemId = itemId;
        this.itemName = itemName;
        this.itemPrice = itemPrice;
        this.datePurchase = datePurchase;
        this.qty=qty;
    }
}

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class Menu extends JFrame {
    String[] beauty={"Flour",
            "Milo","Eggs","Soy Sauce",
            "Nescafe","Dairy Milk Choclate Bar","Milk",
            "Yogurt","Coking Oil"};

    Double[] beautyPrice={5.40,6.20,13.20,4.50,10.00,6.60,7.20,3.80,12.00,};

    

    Menu(Customer customer){
        JPanel panelNorth=new JPanel();
        JPanel panelSouth=new JPanel();
        JLabel jlBeauty=new JLabel("Menu");
        

        JButton jbtPurchase=new JButton("Purchase");
        JButton jbtCancel=new JButton("Cancel");

        panelNorth.setLayout(new GridLayout(25,2));

        panelNorth.add(jlBeauty);
        jlBeauty.setFont(new Font("Verdana", Font.BOLD, 20));
        jlBeauty.setForeground(Color.RED);
        panelNorth.add(new JLabel(""));
        panelNorth.add(new JLabel());
        panelNorth.add(new JLabel());
        for(int i=0;i<beauty.length;i++){
            panelNorth.add(new JLabel(String.format("B%03d >> ",i+1)+beauty[i]));
            panelNorth.add(new JLabel(String.format("RM%.2f",beautyPrice[i])));
        }

        panelNorth.add(new JLabel());
        panelNorth.add(new JLabel());
        panelNorth.add(new JLabel());
        panelNorth.add(new JLabel());
        panelNorth.add(new JLabel());       
        add(panelNorth,BorderLayout.NORTH);
        panelSouth.add(jbtPurchase);
        panelSouth.add(jbtCancel);
        add(panelSouth,BorderLayout.SOUTH);
        setLocationRelativeTo(null);
        setVisible(true);
        setBounds(100,100,650,750);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setTitle("Supermarket Menu");
        jbtPurchase.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                Purchase purchase=new Purchase(customer);
            }
        });
    }

}


import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.ArrayList;
import java.time.LocalDate; // import the LocalDate class

public class Purchase extends JFrame {
    private JLabel jlTitle = new JLabel("Supermarket Purchase");
    private JLabel jlProductCode = new JLabel("Enter Product Code : ");
    private JTextField jtfCode = new JTextField();
    private JLabel jlQty = new JLabel("Quantity");
    private JTextField jtfQty = new JTextField();
    private JButton jbtAddCart = new JButton("Add To Carts");
    private JButton jbtCancel = new JButton("Cancel");
    ArrayList<ItemInformation> carts = new ArrayList<>();

    String[] beauty = {"Flour",
            "Milo", "Eggs", "Soy Sauce",
            "Nescafe", "Dairy Milk Choclate Bar", "Milk",
            "Yogurt", "Cooking Oil" };

    Double[] beautyPrice = {5.40, 6.20, 13.20, 4.50, 10.00, 6.60, 7.20, 3.80, 12.00};

    


    public Purchase(Customer customer) {
        JPanel panelNorth = new JPanel();
        panelNorth.setLayout(new GridLayout(4, 2));
        panelNorth.add(jlTitle);
        panelNorth.add(new JLabel());
        panelNorth.add(new JLabel());
        panelNorth.add(new JLabel());
        jlTitle.setFont(new Font("Verdana", Font.BOLD, 20));
        jlTitle.setForeground(Color.RED);
        panelNorth.add(jlProductCode);
        panelNorth.add(jtfCode);
        panelNorth.add(jlQty);
        panelNorth.add(jtfQty);
        add(panelNorth, BorderLayout.NORTH);


        JPanel panelSouth = new JPanel();
        panelSouth.add(jbtAddCart);
        panelSouth.add(jbtCancel);
        add(panelSouth, BorderLayout.SOUTH);

        jbtAddCart.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                boolean checkValidCode = false;
                for (int i = 0; i < 10; i++) {
                    if (jtfCode.getText().equals(String.format("B%03d", i + 1))) {
                        checkValidCode = true;
                        break;
                    }
                    if (jtfCode.getText().equals(String.format("S%03d", i + 1))) {
                        checkValidCode = true;
                        break;
                    }
                }
                boolean checkInt = false;
                //Validation
                try {
                    int qty = Integer.parseInt(jtfQty.getText());
                    checkInt = true;
                } catch (Exception exception) {
                    checkInt = false;
                }
                if (jtfQty.getText().equals("")) {
                    JOptionPane.showMessageDialog(null, "Please enter quantity");
                }
                if (checkValidCode == false) {
                    JOptionPane.showMessageDialog(null, "Invalid Product Code !");
                } else if (checkInt == false) {
                    JOptionPane.showMessageDialog(null, "Invalid Quantity !");
                } else {
                    for (int i = 0; i < beauty.length; i++) {
                        if (jtfCode.getText().equals(String.format("B%03d", i + 1))) {
                            carts.add(new ItemInformation(jtfCode.getText(), beauty[i], Integer.parseInt(jtfQty.getText()), beautyPrice[i], LocalDate.now()));
                        }
                        
                    }
                    new Cart(customer, carts);
                }
            }
        });
        setLocationRelativeTo(null);
        setVisible(true);
        pack();
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setTitle("Supermarket Info Center");
    }
}

import javax.swing.*;
import javax.swing.border.TitledBorder;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.ArrayList;

public class PaymentInterface extends JFrame {

    private JPanel panel = new JPanel();
    private JRadioButton jrbCC = new JRadioButton("Cash");
    private JRadioButton jrbDC = new JRadioButton("Debit Card");
    private JRadioButton jrbOB = new JRadioButton("Online Banking");
    private ButtonGroup buttonGroup = new ButtonGroup();//Allow one radio button selected

    private JTextField jtfCusName=new JTextField();
    private JTextField jtfTicketTotals=new JTextField();
    private JTextField jtfTotalPrice=new JTextField();
    private JTextField jtfBookingDate=new JTextField();

    private JCheckBox jckAgree = new JCheckBox("Agree");
    private JTextArea jTextArea = new JTextArea("These Terms and Conditions govern the relationship between you as a Customer ('Customer(s)')for providing you an access to purchase items \n" +
            "By purchasing through counter or online transaction, you have unconditionally agreed to be legally bound by these Terms and Conditions that outlined, among other things,\n the refund, exchange and " +
            "cancellation policy together with certain limitations of liability and disclaimers");

    private JButton jbtSubmit = new JButton("Submit");
    private JButton jbtCancel = new JButton("Cancel");


    PaymentInterface(Customer customer, ArrayList<ItemInformation> carts) {
        buttonGroup.add(jrbCC);
        buttonGroup.add(jrbDC);
        buttonGroup.add(jrbOB);

        panel.setBorder(new TitledBorder("Payment Summary"));
        panel.setLayout(new GridLayout(5,4));
        panel.add(new JLabel("Customer Name"));
        jtfCusName.setEditable(false);
        jtfCusName.setText(customer.getName());
        panel.add(jtfCusName);
        panel.add(new JLabel(""));
        panel.add(new JLabel(""));

        panel.add(new JLabel("Total Ordered Purchase"));
        int qty=0;
        for(ItemInformation itemInformation:carts){
            qty+=itemInformation.getQty();
        }
        jtfTicketTotals.setText(String.valueOf(qty));
        jtfTicketTotals.setEditable(false);
        panel.add(jtfTicketTotals);
        panel.add(new JLabel(""));
        panel.add(new JLabel(""));

        //Count ticket price
        double totalPrice=0;
        for(ItemInformation cart:carts){
            totalPrice+=cart.getItemPrice();
        }
        panel.add(new JLabel("Total Price"));
        jtfTotalPrice.setText("RM "+String.format("%.2f",totalPrice*qty));
        jtfTotalPrice.setEditable(false);
        panel.add(jtfTotalPrice);
        panel.add(new JLabel(""));
        panel.add(new JLabel(""));

        panel.add(new JLabel("Purchase Date"));
        jtfBookingDate.setText(String.valueOf(carts.get(0).getDatePurchase()));
        jtfBookingDate.setEditable(false);
        panel.add(jtfBookingDate);
        panel.add(new JLabel(""));
        panel.add(new JLabel(""));


        panel.add(new JLabel("Payment Method"));
        panel.add(jrbCC);
        panel.add(jrbDC);
        panel.add(jrbOB);
        add(panel, BorderLayout.NORTH);

        JPanel panelCenter = new JPanel();
        panelCenter.add(jckAgree);
        panelCenter.add(jTextArea);
        add(panelCenter, BorderLayout.CENTER);
        jckAgree.addActionListener(new radioBtnListener());
        jTextArea.setEditable(false);

        JPanel panelSouth = new JPanel();
        panelSouth.add(jbtSubmit);
        panelSouth.add(jbtCancel);
        

        
        
        jbtSubmit.addActionListener(new ActionListener() {
        @Override
            public void actionPerformed(ActionEvent e) {
                if ((jrbCC.isSelected() || jrbDC.isSelected() || jrbOB.isSelected()) && jckAgree.isSelected()) {
                    int option = JOptionPane.showConfirmDialog(null, "Are you sure to confirm the payment ?");
                    /*if (option == JOptionPane.YES_OPTION) {
                        JOptionPane.showMessageDialog(null,"Counter 1","Thank you for purchase our orders !",JOptionPane.INFORMATION_MESSAGE);
                    }*/
                } else {
                    JOptionPane.showMessageDialog(null,"Please select payment method and check the agree box");
                }
            }            
        });


        
        add(panelSouth, BorderLayout.SOUTH);


        setVisible(true);
        setLocationRelativeTo(null);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setTitle("Payment Gateway");
        pack();

                 //counter set up
        int counter=qty;
        if(counter < 5)
        {
           JOptionPane.showMessageDialog(null,"Proceed to counter 1 or 2"); 
        }
        
        else if(counter >= 5)
        {
            JOptionPane.showMessageDialog(null,"Proceed to counter 3"); 
        }
        
        else 
        {
            JOptionPane.showMessageDialog(null,"Please select payment method and check the agree box");
        }
    }

    public class radioBtnListener implements ActionListener {
        public void actionPerformed(ActionEvent e) {
            if (jckAgree.isSelected()) {
                JOptionPane.showMessageDialog(null, "Terms and conditions agreed");
            }
        }
    }
    


}
