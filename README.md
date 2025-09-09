# Appium
# swip or scroll

package Deemo;

import java.net.MalformedURLException;
import java.net.URI;
import java.net.URL;
import java.time.Duration;
import java.util.Collections;

import org.openqa.selenium.By;
import org.openqa.selenium.Dimension;
import org.openqa.selenium.interactions.Pause;
import org.openqa.selenium.interactions.PointerInput;
import org.openqa.selenium.interactions.Sequence;
import org.openqa.selenium.remote.DesiredCapabilities;

import io.appium.java_client.android.AndroidDriver;

public class SwiporScroll {

	public static void main(String[] args) throws MalformedURLException, InterruptedException {
		// TODO Auto-generated method stub
		DesiredCapabilities capabilities = new DesiredCapabilities();
		capabilities.setCapability("platformName", "Android");
		capabilities.setCapability("appium:platformVersion", "11");
		capabilities.setCapability("appium:deviceName", "Samsung SMA207F");
		capabilities.setCapability("appium:automationName", "uiautomator2");
		capabilities.setCapability("appium:appPackage","io.appium.android.apis");
		capabilities.setCapability("appium:appActivity","io.appium.android.apis.ApiDemos");
		
		URL url = URI.create("http://127.0.0.1:4723/").toURL();
		
		AndroidDriver driver = new AndroidDriver(url,capabilities);
		
		Thread.sleep(5000);
		System.out.println("application started");
		
		//click on view button
		driver.findElement(By.xpath("//android.widget.TextView[@content-desc=\"Views\"]")).click();
		
		//get screen size
		Dimension size = driver.manage().window().getSize();
		
		//find the position where you need to touch
		int startX = size.getWidth() / 2;
		int startY = size.getHeight() / 2;
		
		//position till you want to move your finger to swipe
		int endX = startX;
		int endY = (int) (size.getHeight() * 0.25);
		
		//pointerInput class to create a sequence of actions
		PointerInput finger1 = new PointerInput(PointerInput.Kind.TOUCH, "finger1");
		
		//sequence object, which is a list of actions that will be performed
		Sequence sequence = new Sequence(finger1, 1)
				.addAction(finger1.createPointerMove(Duration.ZERO, PointerInput.Origin.viewport(), startX, startY))
		        .addAction(finger1.createPointerDown(PointerInput.MouseButton.LEFT.asArg()))
		        .addAction(new Pause(finger1, Duration.ofMillis(200)))
		        .addAction(finger1.createPointerMove(Duration.ofMillis(100), PointerInput.Origin.viewport(), endX, endY))
		        .addAction(finger1.createPointerUp(PointerInput.MouseButton.LEFT.asArg()));
		
		//perform the sequence of action
		driver.perform(Collections.singletonList(sequence));
		
		Thread.sleep(2000);
		driver.quit();
		
		

	}

}

--------------------------------------------------------------------
# DropDownHandling

package Deemo;

import java.net.MalformedURLException;
import java.net.URI;
import java.net.URL;
import java.time.Duration;

import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.remote.DesiredCapabilities;

import io.appium.java_client.android.AndroidDriver;

public class DropDownHandling {

    public static void main(String[] args) throws MalformedURLException, InterruptedException {
        DesiredCapabilities capabilities = new DesiredCapabilities();
        capabilities.setCapability("platformName", "Android");
        capabilities.setCapability("appium:platformVersion", "11");
        capabilities.setCapability("appium:deviceName", "Samsung SM-A207F");
        capabilities.setCapability("appium:automationName", "uiautomator2");
        capabilities.setCapability("appium:appPackage", "io.appium.android.apis");
        capabilities.setCapability("appium:appActivity", "io.appium.android.apis.ApiDemos");

        URL url = URI.create("http://127.0.0.1:4723/").toURL();
        AndroidDriver driver = new AndroidDriver(url, capabilities);

        driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));

        System.out.println("Application started");

        // Click on Views (locate fresh each time)
        driver.findElements(By.id("android:id/text1")).get(11).click();

        // Click on Controls (locate fresh again)
        driver.findElement(By.xpath("//android.widget.TextView[@content-desc=\"Controls\"]")).click();

        // Click on Light Theme (locate fresh again)
        driver.findElements(By.id("android:id/text1")).get(0).click();

        // Click on dropdown (locate fresh element)
        driver.findElement(By.id("io.appium.android.apis:id/spinner1")).click();
        
        //select jupitor 
        WebElement jptr = driver.findElements(By.id("android:id/text1")).get(4);
        jptr.click();

        Thread.sleep(5000);
        driver.quit();
    }
}

---------------------------------------------
# AutomateCalculator
package Deemo;

import java.net.MalformedURLException;
import java.net.URI;
import java.net.URL;

import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;

import io.appium.java_client.android.AndroidDriver;
import org.openqa.selenium.remote.DesiredCapabilities;

public class AutomateCalculator {

    public static void main(String[] args) throws MalformedURLException {
        DesiredCapabilities capabilities = new DesiredCapabilities();
        capabilities.setCapability("platformName", "Android");
        capabilities.setCapability("appium:deviceName", "Samsung SM-A207F");
        capabilities.setCapability("appium:automationName", "uiautomator2");
        capabilities.setCapability("appium:platformVersion", "11");
        capabilities.setCapability("appium:appPackage", "com.google.android.calculator");
        capabilities.setCapability("appium:appActivity", "com.android.calculator2.Calculator");

        URL url = URI.create("http://127.0.0.1:4723/").toURL();
        AndroidDriver driver = new AndroidDriver(url, capabilities);

        // addition(8+2)
        WebElement num8 = driver.findElement(By.id("com.google.android.calculator:id/digit_8"));
        num8.click();
        WebElement plus = driver.findElement(By.id("com.google.android.calculator:id/op_add"));
        plus.click();
        WebElement num2 = driver.findElement(By.id("com.google.android.calculator:id/digit_2"));
        num2.click();
        WebElement equal = driver.findElement(By.id("com.google.android.calculator:id/eq"));
        equal.click();
        WebElement result = driver.findElement(By.id("com.google.android.calculator:id/result_final"));
        String resultString = result.getText();

        if (resultString.equals("10")) {
            System.out.println("Pass");
        } else {
            System.out.println("Fail");
        }

        driver.quit();
    }
}

----------------------------------------------------------
# DragAndDropDemo
package Deemo;

import java.net.MalformedURLException;
import java.net.URI;
import java.net.URL;
import java.time.Duration;

import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.remote.DesiredCapabilities;
import org.openqa.selenium.interactions.PointerInput;
import org.openqa.selenium.interactions.Sequence;

import io.appium.java_client.android.AndroidDriver;

import java.util.Arrays;

public class DragAndDropDemo {

    public static void main(String[] args) throws MalformedURLException, InterruptedException {
        // Desired Capabilities
        DesiredCapabilities capabilities = new DesiredCapabilities();
        capabilities.setCapability("platformName", "Android");
        capabilities.setCapability("appium:platformVersion", "11");
        capabilities.setCapability("appium:deviceName", "Samsung SM-A207F");
        capabilities.setCapability("appium:automationName", "uiautomator2");
        capabilities.setCapability("appium:appPackage", "io.appium.android.apis");
        capabilities.setCapability("appium:appActivity", "io.appium.android.apis.ApiDemos");

        // Correct URL (http not https)
        URL url = URI.create("http://127.0.0.1:4723/").toURL();
        AndroidDriver driver = new AndroidDriver(url, capabilities);

        Thread.sleep(5000);
        System.out.println("System started");

        // Click on Views
        WebElement viewBtn = driver.findElements(By.id("android:id/text1")).get(11);
        viewBtn.click();

        // Click on Drag and Drop
        WebElement dragAndDropBtn = driver.findElements(By.id("android:id/text1")).get(7);
        dragAndDropBtn.click();

        // Source and Destination elements
        WebElement source = driver.findElement(By.id("io.appium.android.apis:id/drag_dot_1"));
        WebElement destination = driver.findElement(By.id("io.appium.android.apis:id/drag_dot_2"));

        // Perform Drag and Drop using W3C Actions
        PointerInput finger = new PointerInput(PointerInput.Kind.TOUCH, "finger");
        Sequence dragNDrop = new Sequence(finger, 1);

        // Move finger to source
        dragNDrop.addAction(finger.createPointerMove(Duration.ZERO,
                PointerInput.Origin.fromElement(source), 0, 0));
        dragNDrop.addAction(finger.createPointerDown(PointerInput.MouseButton.LEFT.asArg()));

        // Drag to destination
        dragNDrop.addAction(finger.createPointerMove(Duration.ofMillis(1000),
                PointerInput.Origin.fromElement(destination), 0, 0));
        dragNDrop.addAction(finger.createPointerUp(PointerInput.MouseButton.LEFT.asArg()));

        driver.perform(Arrays.asList(dragNDrop));

        System.out.println("Drag and Drop performed");

        Thread.sleep(5000);
        driver.quit();
    }
}

----------------------------------------
# handletextboxcheckbox
package Deemo;

import java.net.MalformedURLException;
import java.net.URI;
import java.net.URL;

import org.openqa.selenium.By;
import org.openqa.selenium.remote.DesiredCapabilities;

import io.appium.java_client.android.AndroidDriver;

public class handletextBoxCheckboxRadioBtn {

	public static void main(String[] args) throws MalformedURLException, InterruptedException {
		// TODO Auto-generated method stub
		//desiread capabilities
		DesiredCapabilities capabilities = new DesiredCapabilities();
		capabilities.setCapability("platformName", "Android");
		capabilities.setCapability("appium:platformVersion", "11");
		capabilities.setCapability("appium:deviceName", "Samsung SM-A207F");
		capabilities.setCapability("appium:automationName", "uiautomator2");
		capabilities.setCapability("appium:appPackage", "io.appium.android.apis");
		capabilities.setCapability("appium:appActivity", "io.appium.android.apis.ApiDemos");
		
		URL url = URI.create("http://127.0.0.1:4723/").toURL();
		AndroidDriver driver = new AndroidDriver(url,capabilities);
		Thread.sleep(5000);
		System.out.println("Application Started");
		
		//click on views button
		driver.findElements(By.id("android:id/text1")).get(11).click();
		//click on controls button
		driver.findElements(By.id("android:id/text1")).get(4).click();
		//click on light theme
		driver.findElements(By.id("android:id/text1")).get(0).click();
		//enter text in checkbox
		driver.findElement(By.id("io.appium.android.apis:id/edit")).sendKeys("Abhishek pandey");
		//tick on checkbox
		driver.findElement(By.id("io.appium.android.apis:id/check1")).click();
		//click on radiobutton
		driver.findElement(By.id("io.appium.android.apis:id/radio1")).click();
		//click on save button
		driver.findElement(By.id("io.appium.android.apis:id/button")).click();
		
		Thread.sleep(5000);
		driver.quit();
		
		
		
		

	}

}

---------------------------------------
# SwitchingHandling
package Deemo;

import java.net.MalformedURLException;
import java.net.URI;
import java.net.URL;

import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.remote.DesiredCapabilities;

import io.appium.java_client.AppiumBy;
import io.appium.java_client.android.AndroidDriver;

public class SwitchHandling {

    public static void main(String[] args) throws MalformedURLException, InterruptedException {
        // desired capabilities
        DesiredCapabilities capabilities = new DesiredCapabilities();
        capabilities.setCapability("appium:deviceName", "Samsung SM-A207F");
        capabilities.setCapability("platformName", "Android");
        capabilities.setCapability("appium:platformVersion", "11");
        capabilities.setCapability("appium:automationName", "uiautomator2");
        capabilities.setCapability("appium:appPackage", "io.appium.android.apis");
        capabilities.setCapability("appium:appActivity", "io.appium.android.apis.ApiDemos");

        URL url = URI.create("http://127.0.0.1:4723").toURL();
        AndroidDriver driver = new AndroidDriver(url, capabilities);

        Thread.sleep(5000);
        System.out.println("application started");

        // click on "Views" menu (index 11 of main list)
        driver.findElements(By.id("android:id/text1")).get(11).click();

        // scroll to "Switches"
        String MobElementToScroll = "Switches";
        WebElement SwitchElement = driver.findElement(
            AppiumBy.androidUIAutomator(
                "new UiScrollable(new UiSelector().scrollable(true))" +
                ".scrollIntoView(new UiSelector().text(\"" + MobElementToScroll + "\"))"
            )
        );

        // click "Switches"
        SwitchElement.click();

        // toggle the monitored switch
        WebElement monitoredSwitch = driver.findElement(By.id("io.appium.android.apis:id/monitored_switch"));
        
        if (monitoredSwitch.isSelected()==true)
        {
        	System.out.println("Monitored Switch is ON");
        }
        else
        {
        	System.out.println("Monitored Switch is OFF. Doing Switch On");
        	monitoredSwitch.click();
        }

        Thread.sleep(5000);
        driver.quit();
    }
}

----------------------------------------------
# AppManagement
package Deemo;

import java.net.MalformedURLException;
import java.net.URI;
import java.net.URL;

import org.openqa.selenium.remote.DesiredCapabilities;

import io.appium.java_client.android.AndroidDriver;

public class AppManagement {

	public static void main(String[] args) throws MalformedURLException, InterruptedException {
		// TODO Auto-generated method stub
		//Capabilities
		DesiredCapabilities capabilities = new DesiredCapabilities();
		capabilities.setCapability("platformName", "Android");
		capabilities.setCapability("appium:platformVersion", "11");
		capabilities.setCapability("appium:automationName", "uiautomator2");
		capabilities.setCapability("appium:deviceName", "Samsung SMA207F");
		
		URL url = URI.create("http://127.0.0.1:4723/").toURL();
		
		AndroidDriver driver = new AndroidDriver(url,capabilities);
		Thread.sleep(2000);
		
		String packageName = "io.appium.android.apis";
		
		driver.removeApp(packageName);
		
		if(!driver.isAppInstalled(packageName))
		{
			//install application
			driver.installApp("C:\\Users\\HP\\Desktop\\Apk\\ApiDemos-debug.apk");
			System.out.println(" App successfully installed. ");
		}
		else
		{
			System.out.println("App already installed");
			
			
		}
		//activate the application
		driver.activateApp(packageName);
		Thread.sleep(5000);
		driver.quit();
		
	

	}

}



