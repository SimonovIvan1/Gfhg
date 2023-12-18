package paint; 
import java.awt.*; 
import java.awt.event.*; 
import javax.swing.*; 
 
//Класс, расширяющий JPanel и реализующий интерфейсы 
//ActionListener - слушатель событий лействия 
//MouseListener - слушатель событий мыши 
//MouseMotionListener - слушатель событий перемещения мыши 
public class PaintPanel extends JPanel implements ActionListener, MouseListener, 
 MouseMotionListener, MouseWheelListener { 
 private static final long serialVersionUID = 1L; 
 public static float wl = 5.0F; 
 protected int lastX, lastY, w, h; 
 protected Color curColor = Color.BLACK; 
 protected JFrame f; 
 
 JLabel curSizeLabel; 
 
//Конструктор. Принимает в качестве параметров фрейм, на котором будет 
// размещена 
 //панель и размеры панели 
 public PaintPanel(JFrame frame, int width, int height) { 
 super(); 
 f = frame; 
 w = width; 
 h = height; 
 curSizeLabel = new JLabel("Размер пера:" + wl); 
 frame.add(curSizeLabel, BorderLayout.NORTH); 
 } 
 public void setCurColor(Color newColor){ 
 curColor = newColor; 
 } 
 //Обработчик события перемещения мыши с нажатой кнопкой 
 @Override 
 public void mouseDragged(MouseEvent me) { 
//Если при перемещении нажата левая кнопка мыши 
 if ((me.getModifiers() & MouseEvent.BUTTON1_MASK) == 
 MouseEvent.BUTTON1_MASK) { 
//С поммощью вызова метода this.getGraphics() получаем графический 
// контекст нашей панели 
//и приводим его к Graphics2D 
 Graphics2D g2 = (Graphics2D)this.getGraphics(); 
//Устанавливаем текущую ширина штриха (Stroke) в 5 пикселей 
 g2.setStroke(new BasicStroke(wl, BasicStroke.CAP_ROUND, 
 BasicStroke.JOIN_BEVEL)); 
 g2.setRenderingHint(RenderingHints.KEY_ANTIALIASING, 
 RenderingHints.VALUE_ANTIALIAS_ON); 
//Устанавливаем текущий цвет рисования 
 g2.setColor(curColor); 
//Рисуем текущим штрихом и цветом прямую линию от предыдущего 
//положения мыши до текущего 
 
 g2.drawLine(lastX, lastY, me.getX(), me.getY()); 
//Телаем текущее положение мыши предыдущим 
 lastX = me.getX(); 
 lastY = me.getY(); 
 } 
 } 
 @Override 
 //Обработка вращения колесика мыши 
 public void mouseWheelMoved(MouseWheelEvent mwe) { 
// Метод возвращает положительное значение, если колесико мыши 
// вращается на себя 
// и отрицательное, если вращение происходит от себя 
 if ((mwe.getWheelRotation() > 0) && (wl < 50)) 
 wl = wl + 1; 
 curSizeLabel.setText("Размер пера:" + wl); 
 if ((mwe.getWheelRotation() < 0) && (wl > 5)) 
 wl = wl - 1; 
 curSizeLabel.setText("Размер пера:" + wl); 
 System.out.println("Размер пера: " + wl); 
 } 
 //Это событие не обработано 
 @Override 
 public void mouseMoved(MouseEvent e) {} 
 //Это событие не обработано 
 @Override 
 public void mouseClicked(MouseEvent arg0) {} 
 //Это событие не обработано 
 @Override 
 public void mouseEntered(MouseEvent arg0) {} 
 //Это событие не обработано 
 @Override 
 public void mouseExited(MouseEvent arg0) {} 
 //Обработчик события нажания мыши 
 @Override 
 public void mousePressed(MouseEvent me) { 
//Если нажата левая кнопка мыши 
 if ((me.getModifiers() & MouseEvent.BUTTON1_MASK) == 
 MouseEvent.BUTTON1_MASK) { 
//устанавливаем предыдущие координаты мыши в текущие 
 lastX = me.getX(); 
 lastY = me.getY(); 
 } 
 } 
 
//Это событие не обработано 
 @Override 
 public void mouseReleased(MouseEvent arg0) {} 
 //Обработчик события действия. Применяется здесь для 
//обработки нажатий на кнопки 
 @Override 
 public void actionPerformed(ActionEvent event) { 
 String s = event.getActionCommand(); 
 if (s.equals("Change color")) curColor = JColorChooser.showDialog(null , "Select a Color", Color.BLACK); 
 } 
}
