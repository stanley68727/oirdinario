import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class CalculadoraEcuacionCuadratica extends JFrame {
    private JTextField textFieldA, textFieldB, textFieldC;
    private JLabel labelResultado;

    public CalculadoraEcuacionCuadratica() {
        // Configurar el marco principal
        setTitle("Calculadora de Ecuacion Cuadratica");
        setSize(400, 200);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);

        // Crear un panel para organizar los elementos
        JPanel panel = new JPanel();
        panel.setLayout(new GridLayout(4, 2, 10, 10));

        // Crear etiquetas y campos de texto
        JLabel labelA = new JLabel("A:");
        JLabel labelB = new JLabel("B:");
        JLabel labelC = new JLabel("C:");
        labelResultado = new JLabel("Resultado:");
        textFieldA = new JTextField();
        textFieldB = new JTextField();
        textFieldC = new JTextField();

        // Crear botones "Calcular" y "Limpiar"
        JButton calcularButton = new JButton("Calcular");
        JButton limpiarButton = new JButton("Limpiar");

        // Agregar componentes al panel
        panel.add(labelA);
        panel.add(textFieldA);
        panel.add(labelB);
        panel.add(textFieldB);
        panel.add(labelC);
        panel.add(textFieldC);
        panel.add(labelResultado);
        panel.add(calcularButton);
        panel.add(limpiarButton);

        // Agregar el panel al marco principal
        add(panel);

        // Configurar el manejador de eventos para el boton "Calcular"
        calcularButton.addActionListener(new ActionListener() {
            @override
            public void actionPerformed(ActionEvent e) {
                calcularEcuacionCuadratica();
            }
        });

        // Configurar el manejador de eventos para el boton "Limpiar"
        limpiarButton.addActionListener(new ActionListener() {
            @override
            public void actionPerformed(ActionEvent e) {
                limpiarCampos();
            }
        });
    }

    private void calcularEcuacionCuadratica() {
        try {
            double a = Double.parseDouble(textFieldA.getText());
            double b = Double.parseDouble(textFieldB.getText());
            double c = Double.parseDouble(textFieldC.getText());

            double discriminante = b * b - 4 * a * c;

            if (discriminante < 0) {
                labelResultado.setText("No hay soluciones reales.");
            } else if (discriminante == 0) {
                double x = -b / (2 * a);
                labelResultado.setText("La solucion es x = " + x);
            } else {
                double x1 = (-b + Math.sqrt(discriminante)) / (2 * a);
                double x2 = (-b - Math.sqrt(discriminante)) / (2 * a);
                labelResultado.setText("Las soluciones son x1 = " + x1 + " y x2 = " + x2);
            }
        } catch (NumberFormatException e) {
            labelResultado.setText("Ingrese valores validos en A, B y C.");
        }
    }

    private void limpiarCampos() {
        textFieldA.setText("");
        textFieldB.setText("");
        textFieldC.setText("");
        labelResultado.setText("Resultado:");
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            @Override
            public void run() {
                new CalculadoraEcuacionCuadratica().setVisible(true);
            }
        });
    }
}




