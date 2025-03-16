# task11
nested frame
import org.apache.commons.io.FileUtils;
import org.openqa.selenium.By;
import org.openqa.selenium.OutputType;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver; 
import org.openqa.selenium.TakesScreenshot;

import java.io.File;
import java.io.IOException;

public class Nestedframes {
    public static void main(String[] args) throws IOException {
     
        WebDriver driver = new ChromeDriver(); 
        TakesScreenshot screenshot=(TakesScreenshot) driver;
        File one=screenshot.getScreenshotAs(OutputType.FILE);
        File fileone= new File("C:\\Users\\wel come\\eclipse-workspace\\Task11\\Screenshot\\1.0.jpg");
        FileUtils.copyFile(one, fileone);	

        try {
            
            driver.get("http://the-internet.herokuapp.com/nested_frames");

            TakesScreenshot screenshot1=(TakesScreenshot) driver;
            File two=screenshot1.getScreenshotAs(OutputType.FILE);
            File filetwo= new File("C:\\Users\\wel come\\eclipse-workspace\\Task11\\Screenshot\\2.0.jpg");
            FileUtils.copyFile(two, filetwo);
            driver.switchTo().frame("frame-top");

            
            int numberOfFrames = driver.findElements(By.tagName("frame")).size();
            if (numberOfFrames == 3) {
                System.out.println("Verified: There are three frames on the page.");
            } else {
                System.out.println("Verification failed: Expected 3 frames, found " + numberOfFrames);
            }
            TakesScreenshot screenshot2=(TakesScreenshot) driver;
            File three=screenshot2.getScreenshotAs(OutputType.FILE);
            File filethree= new File("C:\\Users\\wel come\\eclipse-workspace\\Task11\\Screenshot\\3.0.jpg");
            FileUtils.copyFile(three, filethree);
            
            driver.switchTo().frame("frame-left");

            
            String leftFrameText = driver.getPageSource();
            if (leftFrameText.contains("LEFT")) {
                System.out.println("Verified: The left frame contains the text 'LEFT'.");
            } else {
                System.out.println("Verification failed: The left frame does not contain the text 'LEFT'.");
            }

            TakesScreenshot screenshot3=(TakesScreenshot) driver;
            File four=screenshot3.getScreenshotAs(OutputType.FILE);
            File filefour= new File("C:\\Users\\wel come\\eclipse-workspace\\Task11\\Screenshot\\4.0.jpg");
            FileUtils.copyFile(four, filefour);
            driver.switchTo().parentFrame();
            
            driver.switchTo().frame("frame-middle");

             String middleFrameText = driver.getPageSource();
            if (middleFrameText.contains("MIDDLE")) {
                System.out.println("Verified: The middle frame contains the text 'MIDDLE'.");
            } else {
                System.out.println("Verification failed: The middle frame does not contain the text 'MIDDLE'.");
            }
            TakesScreenshot screenshot4=(TakesScreenshot) driver;
            File five=screenshot4.getScreenshotAs(OutputType.FILE);
            File filefive= new File("C:\\Users\\wel come\\eclipse-workspace\\Task11\\Screenshot\\5.0.jpg");
            FileUtils.copyFile(five, filefive);
            
            driver.switchTo().parentFrame();

            
            driver.switchTo().frame("frame-right");

            
            String rightFrameText = driver.getPageSource();
            if (rightFrameText.contains("RIGHT")) {
                System.out.println("Verified: The right frame contains the text 'RIGHT'.");
            } else {
                System.out.println("Verification failed: The right frame does not contain the text 'RIGHT'.");
            }
            TakesScreenshot screenshot5=(TakesScreenshot) driver;
            File six=screenshot5.getScreenshotAs(OutputType.FILE);
            File filessix= new File("C:\\Users\\wel come\\eclipse-workspace\\Task11\\Screenshot\\6.0.jpg");
            FileUtils.copyFile(six, filessix);
           
            driver.switchTo().parentFrame();

           
            driver.switchTo().frame("frame-bottom");

            
            String bottomFrameText = driver.getPageSource();
            if (bottomFrameText.contains("BOTTOM")) {
                System.out.println("Verified: The bottom frame contains the text 'BOTTOM'.");
            } else {
                System.out.println("Verification failed: The bottom frame does not contain the text 'BOTTOM'.");
            }

            TakesScreenshot screenshot6=(TakesScreenshot) driver;
            File seven=screenshot6.getScreenshotAs(OutputType.FILE);
            File fileseven= new File("C:\\Users\\wel come\\eclipse-workspace\\Task11\\Screenshot\\7.0.jpg");
            FileUtils.copyFile(seven, fileseven);
            
            driver.switchTo().parentFrame();

        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            
            driver.quit();
        }
    }
}



Switching Window

import org.apache.commons.io.FileUtils;
import org.openqa.selenium.By;
import org.openqa.selenium.OutputType;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;
import org.openqa.selenium.TakesScreenshot;

import java.io.File;
import java.time.Duration;
import java.util.ArrayList;
public class Newwindow {

	public static void main(String[] args)  {    
		        WebDriver driver = new ChromeDriver(); 
		        
		        try {
		            
		            driver.get("https://the-internet.herokuapp.com/windows");
		          
		            WebElement clickHereButton = driver.findElement(By.linkText("Click Here"));
		            clickHereButton.click();
		            
		            	TakesScreenshot screenshot=(TakesScreenshot) driver;
			            File one=screenshot.getScreenshotAs(OutputType.FILE);
			            File fileone= new File("C:\\Users\\wel come\\eclipse-workspace\\Task11\\Screenshot\\1.jpg");
			            FileUtils.copyFile(one, fileone);		
			            
             WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(30));
		            wait.until(ExpectedConditions.numberOfWindowsToBe(2));

		          
		            ArrayList<String> windowHandles = new ArrayList<>(driver.getWindowHandles());
		            driver.switchTo().window(windowHandles.get(1)); 

		           
		            String pageTitle = driver.getTitle();
		            if (pageTitle.equals("New Window")) {
		                System.out.println("Successfully switched to the new window and verified the title.");
		            } else {
		                System.out.println("Failed to verify the new window title.");
		            }
		            TakesScreenshot screenshot1=(TakesScreenshot) driver;
		            File two=screenshot1.getScreenshotAs(OutputType.FILE);
		            File filetwo= new File("C:\\Users\\wel come\\eclipse-workspace\\Task11\\Screenshot\\2.jpg");
		            FileUtils.copyFile(two, filetwo);
		            driver.close();
		            driver.switchTo().window(windowHandles.get(0));

		            String originalPageTitle = driver.getTitle();
		            if (originalPageTitle.equals("The Internet")) {
		                System.out.println("Successfully switched back to the original window.");
		            } else {
		                System.out.println("Failed to switch back to the original window.");
		            }

		        } catch (Exception e) {
		            e.printStackTrace();
		        } finally {
		           
		            driver.quit();
		        }
		    }
		

	}
