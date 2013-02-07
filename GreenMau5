
/*
 * @author: Ethan Green
 * 
 * This program is an adaptation of the work started by Noah Huppert
 * The way in which the x and y locations are found on the screen has
 * been changed as well as the way clicking works. Scrolling was removed
 * for the time being.
 * 
 */
import java.awt.AWTException;
import java.awt.Robot;
import java.awt.event.InputEvent;
import com.leapmotion.leap.*;

public class MouseTesting{
	// time is the sleep time interval on the animation of the mouse movement.
	// smoothing is the number of intervals taken during the animation.
	// count is the number of iterations the while loop must take before it selects a new frame.
	final static int time = 0;
	final static int smoothing = 1;
	final static int count = 2;
	Listener listener = new Listener();
	Controller controller = new Controller();

	/*
	 *  Code by Ethan Green
	 *  Leap's X range -200 to +200 -> normalize to 0-400
	 *  Leap's Y range ~40 to ~400 -> normalize to 40-400
	 *  
	 *  For increased sensitivity there will only be a 100
	 *  on the tip position for both x and y to make it easier
	 *  to move the mouse around the screen.
	 */
	
	public static void main (String[] args) throws InterruptedException, AWTException 
	{
		Robot robot = new Robot();
		Controller controller = new Controller();
		int counter = 0;
		int x2 = 0;
		int y2 = 0;
		
		while(true) {
			counter ++;
			Frame frame = controller.frame();
			Finger finger = frame.fingers().get(0);
			ScreenList screenList = controller.calibratedScreens();
			Screen screen = screenList.get(0);
			
			if(counter == 1){
				x2 = (int) finger.tipPosition().getX() + 100;
				y2 = (int) finger.tipPosition().getY() - 75;
			} else if(counter == count){
			
					if(frame.fingers().count() == 1){
						int xPos = (int) finger.tipPosition().getX() + 100;
						int yPos = (int) finger.tipPosition().getY() - 75;
						
						double relativeX1 = inBounds(xPos / 200.0);
						double relativeY1 = inBounds(-1 * ((yPos / 175.0)-1));
						double relativeX2 = inBounds(x2 / 200.0);
						double relativeY2 = inBounds(-1 * ((y2 / 175.0)-1));
						
						
						// Set the location based on the pixels on the screen.
						int screenX1 = (int) (relativeX1 * screen.widthPixels());
						int screenY1 = (int) (relativeY1 * screen.heightPixels());
						
						int screenX2 = (int) (relativeX2 * screen.widthPixels());
						int screenY2 = (int) (relativeY2 * screen.heightPixels());
						
						// For animation uncomment this line.
						mouseGlide(screenX1, screenY1, screenX2, screenY2, time, smoothing, robot);
						//robot.mouseMove(screenX2, screenY2);
						counter = 0;
					}
					
					else if(frame.fingers().count() == 3) {
						
						robot.mousePress(InputEvent.BUTTON1_MASK);
						Thread.sleep(600);
						robot.mouseRelease(InputEvent.BUTTON1_MASK);
						counter = 0;
					} else if(frame.fingers().count() >= 8) {
						break;
					} else{
						counter = 0;
					}
			}	
		}
    }
	
	// Credit to Andy Zhang via Stack Overflow.
	public static void mouseGlide(int x1, int y1, int x2, int y2, int t, int n, Robot r) {
	    try {
	        double dx = (x2 - x1) / ((double) n);
	        double dy = (y2 - y1) / ((double) n);
	        double dt = t / ((double) n);
	        for (int step = 1; step <= n; step++) {
	            Thread.sleep((int) dt);
	            r.mouseMove((int) (x1 + dx * step), (int) (y1 + dy * step));
	        }
	    } catch (InterruptedException e) {
	        e.printStackTrace();
	    }
	}
	
	public static double inBounds(double i){
		if(i > 1){
			return 1;
		} else if (i < 0){
			return 0;
		} else{
			return i;
		}
	}
}
