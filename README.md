# Sample_menu
a piece of code that displays a menu with three buttons, after clicking on the a dialog box with message pops out

    package simple_menu;

    import javax.swing.*;
    import java.awt.*;
    import java.awt.event.*;

    public class Main extends JFrame {

    private Container kontener = this.getContentPane();
    private JPanel panelMenu = new JPanel();
    private MenuButton mButton1 = new MenuButton("1. Dodaj");
    private MenuButton mButton2 = new MenuButton("2. Usuń");
    private MenuButton mButton3 = new MenuButton("3. Zmień");
    private int i = 0;
    
    
    public Main()
    {
        initComponents();
    }
    
    public void initComponents()
    {
        this.setTitle("Przykładowe menu");
        this.setBounds(200,200,400,200);
        
        panelMenu.setLayout(new GridLayout(3,1));
        panelMenu.add(mButton1);
        panelMenu.add(mButton2);
        panelMenu.add(mButton3);
        
        kontener.add(panelMenu);
               
        this.setDefaultCloseOperation(3);
               
    }
    
    private class MenuButton extends JButton implements FocusListener, ActionListener
    {
        public MenuButton (String nazwa) 
        {
            super(nazwa);
            this.setBackground(Color.BLUE);
            this.addFocusListener(this);
            this.addActionListener(this);
            this.addKeyListener(new KeyAdapter() {
                
                @Override
                public void keyPressed(KeyEvent e) {
                    keyPressedHandler(e);
                }
            });
         
        }
        
        private Color kFocusGained = Color.YELLOW;
        private Color kFocusLost = Color.BLUE;
        
    

        @Override
        public void focusGained(FocusEvent e) {
            this.setBackground(kFocusGained);
        }

        @Override
        public void focusLost(FocusEvent e) {
            this.setBackground(kFocusLost);
 
        }
        
        private void keyPressedHandler(KeyEvent e)
        {
            int dlMenu = panelMenu.getComponentCount();
            
            if (i == 0) i = 10*dlMenu;
            if(e.getKeyCode() == KeyEvent.VK_DOWN)
            {
               panelMenu.getComponent(++i % dlMenu).requestFocus();
            }
            else if (e.getKeyCode() == KeyEvent.VK_UP)
            {
               panelMenu.getComponent(--i % dlMenu).requestFocus();
            }
            else if (e.getKeyCode() == KeyEvent.VK_ENTER)
            {
               ((MenuButton)e.getSource()).doClick();
            }
            
        }

        @Override
        public void actionPerformed(ActionEvent e) {
            JOptionPane.showMessageDialog(this, ((MenuButton)e.getSource()).getText());
        }
    }
    
    public static void main(String[] args) {
       
        new Main().setVisible(true);
        
    }


    }
